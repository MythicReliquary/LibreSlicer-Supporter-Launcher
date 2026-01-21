# Revocation Updates (Commercial / Term Licenses, Offline)

LibreSlicer Supporter Tools are designed to run fully offline (zero telemetry). Because the software cannot "phone home", **term (subscription) licenses require a signed revocation list file** so compromised/stolen keys can be invalidated over time.

## What you get
For Commercial/Indie deployments you will receive:
- `license.key` (signed license token)
- `revoked_keys.json` (signed revocation list)

## Where to place `revoked_keys.json`
Release builds look for `revoked_keys.json` in:
1) The same folder as the `license.key` you pass via `--license-key`, or
2) The current working directory.

If a term license is used and `revoked_keys.json` is missing/invalid, the CLI fails closed.

## How to update in an air-gapped environment
1) On an internet-connected machine, obtain the latest `revoked_keys.json` from the vendor.
2) Copy `revoked_keys.json` to the offline machine(s) that run the CLI.
3) Place it next to the `license.key` (recommended).
4) Verify the license still validates:
```powershell
.\devpacks-cli.exe license-verify .\license.key --out .\license_report.json
```

## Recommended operational policy
- Keep a copy of the last-known-good `revoked_keys.json` in your change control / backup system.
- Update `revoked_keys.json` on a schedule aligned to your risk posture (e.g., monthly/quarterly), or immediately after an incident.
- If the offline machine is reimaged or moved, re-copy both `license.key` and `revoked_keys.json`.

Questions: `support@mythicreliquary.com`.


