# RC-W1-07 — G2 QA Toolchain Discovery: JSON Object-Key Parser Failure and Read-Only Recovery

> **Observed:** 2026-10-12T19:23:35.8238929+07:00 (owner PowerShell output).
> **Evidence:** OWNER_POWERSHELL_OUTPUT. Reviewer independently inspected Studio GitHub `package.json` and `package-lock.json` from approved Studio `main` SHA `18b295f96ccb521b228a1855e79448158c09db15`. No independent execution on owner's Windows machine.
> **Current state:** `G1 APPROVED`, `G2 SOURCE REVIEW PASS_SCOPED`, `W1 RUNTIME QA BLOCKED_DEPENDENCIES`, `G3 NOT AUTHORIZED`.
> **Contract:** [RC-W1-01](./RC-W1-01-proposed-g2-first-contact-creator-reader-ia-work-order-20261012.md), [RC-W1-03 G2 owner approval](./RC-W1-03-owner-g2-ratification-and-isolated-execution-20261012.md), [RC-W1-06 source-review classification](./RC-W1-06-independent-source-review-g2-implementation-and-qa-blockers-20261012.md).
> **No software installation, source edits, cache cleanup, Git operations beyond read-only status, paid provider calls, push/PR/preview/production.**

## 1. Successfully observed before the failure

- Isolated path `C:\Projects\reltroner-studio-w1-ia`, local branch `phase1/w1-creator-reader-ia-20261012`; `HEAD 18b295f96ccb521b228a1855e79448158c09db15` exact matches approved G2.
- Git working tree shows only three previously authorized tracked modifications: `app/page.tsx`, `components/ecosystem/EcosystemHero.tsx`, `components/ecosystem/UseCasePathways.tsx`. No new tracked or untracked changes were reported.
- `package-lock.json=True`; `bun.lock=True`; `pnpm-lock.yaml=False`; `yarn.lock=False`.
- `node_modules=False`; Node `v22.23.1`; npm `10.9.8`; Bun not installed.
- Root `package.json` contains `"learn-nextjs": "file:"`. This is an unusual local-package spec that may affect future reproducible installation; it is a **risk to inspect**, not proven install failure.
- A GitHub read-only check of the exact baseline lock confirmed `lockfileVersion: 3` and `packages[""]` with root name `learn-nextjs`. This was not returned by the interrupted owner script.

## 2. Exact cause of stop

The previous RC-W1-07 script used:

```powershell
$Lock = Get-Content -LiteralPath $LockPath -Raw | ConvertFrom-Json
Write-Host "npm root name = $($Lock.packages.'').name"
```

The owner observed:

```text
ConvertFrom-Json: The provided JSON includes a property whose name is an empty string,
this is only supported using the -AsHashTable switch.
```

The npm lockfile specification uses the empty-string key `packages[""]` for the root package. In PowerShell 7, the `ConvertFrom-Json -AsHashtable` option permits empty keys; **Windows PowerShell 5.1 does not provide this switch**. Therefore the durable, cross-edition correction is to parse the lockfile with the already verified Node.js 22 runtime using read-only `fs.readFileSync` + `JSON.parse`.

**Classification:** `RC_W1_07=PARTIAL_SCRIPT_STOP_JSON_PARSER`, not `APP_SOURCE_ERROR`, not `LOCKFILE_INVALID`, and not `COMPLETE_READ_ONLY`. Because PowerShell `$ErrorActionPreference='Stop'` halted at JSON parsing, disk-space output and the end marker were not produced.

## 3. Approved read-only continuation (operator may execute without new G2 authorization)

The user-facing response provides the complete corrected `RC-W1-07R` PowerShell 5.1/7-compatible block. Critical logic is:

```powershell
$LockPath = 'C:\Projects\reltroner-studio-w1-ia\package-lock.json'
$PackagePath = 'C:\Projects\reltroner-studio-w1-ia\package.json'
$JavaScript = @'
const fs = require("node:fs");
const lock = JSON.parse(fs.readFileSync(process.argv[1], "utf8"));
const pkg = JSON.parse(fs.readFileSync(process.argv[2], "utf8"));
const root = lock.packages?.[""];
if (!root) process.exit(2);
console.log("npm lockfileVersion = " + lock.lockfileVersion);
console.log("npm root name = " + root.name);
console.log("package root name = " + pkg.name);
console.log("package learn-nextjs = " + pkg.dependencies?.["learn-nextjs"]);
console.log("lock root learn-nextjs = " + root.dependencies?.["learn-nextjs"]);
'@
& node -e $JavaScript $LockPath $PackagePath
if ($LASTEXITCODE -ne 0) { throw 'STOP: JSON inspection failed' }
```

The delivered full operator block additionally checks exact branch/HEAD, root dependency spec alignment and local file self-reference entry, disk free space and source Git status, then prints `RC_W1_07R=COMPLETE_READ_ONLY` only on completion.

**Caution:** A match of root dependency declaration specs does not validate all lockfile tarball integrity, lifecycle, native binaries or package-manager compatibility. Do **not** use this as authority to run `npm ci` or `bun install`.

## 4. Gate / next step

- **No new G2 permission required** to finish read-only discovery; the prior failure had no installation side effect.
- Await actual `RC_W1_07R=COMPLETE_READ_ONLY` output before designing a bounded W1 QA dependency setup.
- Any future `npm ci`, `bun` installation, Node toolchain upgrade, external binary downloads, symlink/copy `node_modules`, lockfile changes or test-run deployment needs a **distinct owner G2-QA authorization**, with the `"file:"` dependency risk evaluated.
- Existing local W1 patch remains uncommitted/unpushed; G3–G8 hold; all 27 WEB acceptance remain binding.
