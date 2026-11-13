# openNDS for OpenWrt 25.12.6 (MediaTek Filogic)

This repository builds the official openNDS **11.0.0** source for:

- OpenWrt: 25.12.6
- Target: mediatek/filogic
- Package architecture: aarch64_cortex-a53
- Package format: APK

The build runs in GitHub Actions; no Linux or WSL installation is required on the local PC.

## Build

The workflow starts automatically when the build recipe or workflow changes on `main`, and can also be started manually from **Actions → Build openNDS for OpenWrt 25.12.6 → Run workflow**.

The workflow verifies the official OpenWrt SDK SHA-256 and verifies that the official openNDS v11.0.0 tag resolves to the pinned upstream commit before building.

## Output

Download the artifact named `opennds-11.0.0-openwrt-25.12.6-mediatek-filogic` from the completed workflow run. It contains the APK and a SHA-256 checksum file.

**Do not install the package until the build has completed successfully and the resulting APK has been checked against the router's installed dependencies and configuration.**
