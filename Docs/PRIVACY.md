# Privacy Policy (Zero Telemetry)

**Effective date:** 2025-12-01  
**Applies to:** Dev_Packs CLI tools, any local UI components included with your bundle (e.g., launcher and/or local UI assets), and any vendor-provided Docker images.

## Summary
LibreSlicer Supporter Bundle is designed to run fully offline. The software does not include telemetry, analytics, tracking, or advertising SDKs, and it does not automatically transmit your files, models, logs, or usage data to Mythic Reliquary or third parties.

## What data the software collects
The software does not collect personal data for telemetry purposes.

## What data the software processes
The software processes the files you provide (e.g., model files, project configuration files) and produces outputs on your machine (e.g., repaired meshes, supports, QA reports, simulation artifacts).

All processing is performed locally unless you choose to move data elsewhere.

## Network access
- No auto-updater and no background "phone home" behavior.
- No telemetry endpoints.
- If you use an optional workflow that requires a network resource (for example, pulling a container image with your own tooling), that network activity is under your control and outside the software's telemetry design.

## Licenses and offline revocation updates
Some commercial/term licenses require a signed revocation list file (`revoked_keys.json`) to be present (fail-closed). You (or your organization) obtain the file out-of-band and copy it to offline machines as needed; the software does not fetch it automatically. See `REVOCATION_UPDATES.md`.

## Emails and support requests
If you contact support (for example, by email), the contents of your message and any attachments are handled like normal email correspondence and may include personal data you choose to provide.

## Third-party components
The bundle may include third-party components that remain under their respective licenses. This privacy policy describes the intended behavior of the bundle as distributed; your operating system, drivers, security software, or other third-party tools may independently collect data.

## Changes
This policy may be updated in future releases. The effective date will be revised when changes are made.

## Contact
Questions: support@mythicreliquary.com
