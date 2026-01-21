# LibreSlicer Supporter Bundle - Setup Guide (Offline-Friendly)

This bundle is designed to run fully offline (zero telemetry). Nothing is uploaded; there is no auto-updater.

Privacy policy: `PRIVACY.md`.

## 1) What you installed
- `devpacks-cli.exe`: Headless CLI tools (repair, hollowing, supports, QA, simulations, etc.).
- `LSSBLauncher.exe` (optional): A local UI that runs the CLI on your machine (no network).
- `profiles/`: Offline material profiles/presets.
- License and terms: `EULA.individual.md`, `EULA.commercial.md`, `EULA.md`.

## 2) System requirements (Windows)
- Windows 10/11 x64.
- No admin required.
- If Windows reports missing MSVC runtime DLLs (e.g., `VCRUNTIME140_1.dll`), install the Microsoft Visual C++ Redistributable 2015-2022 (x64).

## 3) Verify your download (recommended, offline)
In PowerShell, from the folder that contains `SHA256SUMS`:
```powershell
Get-Content .\SHA256SUMS | ForEach-Object {
  if ($_ -match '^([a-f0-9]{64})\\s\\s(.+)$') {
    $expected = $matches[1].ToLowerInvariant()
    $file = $matches[2]
    $actual = (Get-FileHash -Algorithm SHA256 -Path $file).Hash.ToLowerInvariant()
    if ($actual -ne $expected) { throw "SHA256 mismatch: $file" }
  }
}
"OK"
```

## 4) Licensing overview (what end users need to know)
Your bundle may be distributed as separate tiers, but the binaries can be identical. The license determines permitted use.

- **Evaluation / Trial**: available from the vendor (or an authorized distributor) for prospective customers to try before purchasing. See `EULA.md`. To request an evaluation copy, email `support@mythicreliquary.com`.
- **Personal (Individual / Non-Commercial)**: perpetual (non-expiring) license for use that does not generate revenue. See `EULA.individual.md`.
- **Indie/Commercial (Business Use)**: term (subscription) license for internal business use and revenue-generating work. See `EULA.commercial.md`.

Tiers also map to support/SLA engagement levels (`SLA.md`). Purchases at lower tiers can fund development of higher-tier workflows/features, but the software does not enforce feature gating by tier (terms and support differ, not the binaries).

Questions: `support@mythicreliquary.com`.

## 5) License files you may receive
You will typically be provided:
- `license.key`: your signed license token (keep private).

Some deployments also include:
- `revoked_keys.json`: signed revocation list used to invalidate compromised/stolen term licenses.
- `compliance_public.jwk.json`: the public key used to verify compliance/material-lot manifests (only needed if you use compliance features).

## 6) Where to put the license (offline activation)
Recommended: keep a per-job folder that contains your `project.json` and the license files.

Example folder layout:
```
MyJob\
  project.json
  license.key
  revoked_keys.json        (Commercial/term licenses only)
  artifacts\               (output folder you choose)
```

Then run the CLI with an explicit license path:
```powershell
.\devpacks-cli.exe license-verify .\license.key --out .\license_report.json
```

If the license is valid, you can run workflows like:
```powershell
.\devpacks-cli.exe personal .\project.json --license-key .\license.key --output .\bundle_summary.json --artifact-dir .\artifacts
```

## 7) Revocation list (Commercial/term licenses)
For **term licenses**, Release builds require a valid `revoked_keys.json` (fail-closed). This is what keeps stolen keys from working forever in a zero-telemetry product.

Where the app looks:
- Next to the `license.key` you pass, or
- In the current working directory.

Air-gapped update flow:
- You (or your IT/security office) periodically obtain the latest `revoked_keys.json` from the vendor and copy it to your offline machine(s).
- See `REVOCATION_UPDATES.md` for a copy/paste procedure.

## 8) Compliance/material-lot verification (optional)
Some regulated workflows use a material lot manifest (`--material-lot-manifest ...`) and require a compliance public key file.

Release builds will look for one of these filenames next to `devpacks-cli.exe` or in the current working directory:
- `compliance_public.jwk.json`
- `compliance_public_jwk.json`
- `compliance_public_key.jwk.json`
- `compliance_public_key.json`

If you don't use compliance commands/features, you can ignore this.

## 9) Using the launcher (optional)
- Run `LSSBLauncher.exe` (tray icon appears).
- Tray menu -> open the Command Palette.
- Choose a workflow (Repair / Hollow / Supports / QA / Simulations), select your input file(s), then run.

## 10) Troubleshooting
- License rejected: confirm you're using the correct tier (`EULA.individual.md` vs `EULA.commercial.md`), and re-run `license-verify` to see the reason.
- Commercial license rejected offline: ensure `revoked_keys.json` is present and up-to-date.
- Hardware change/reimage: licenses may be hardware-bound; email `support@mythicreliquary.com`.
