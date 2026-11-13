# openNDS 11.0.0 for OpenWrt 25.12.6 (MediaTek Filogic)

This repository builds the official openNDS **11.0.0** source for the OpenWrt SDK target:

- OpenWrt SDK: **25.12.6**
- Target: **mediatek/filogic**
- Package architecture: **aarch64_cortex-a53**
- Output format: **APK**
- openNDS source: official tag \`v11.0.0\`, pinned to commit \`9477b224bfd6d7f27ab1f1931afb61580b9470d1\`

The build runs in GitHub Actions. No Linux, Ubuntu, WSL, or compiler is required on the local PC.

## Why the build uses a local MHD recipe

openNDS depends on \`libmicrohttpd-no-ssl\`. The upstream OpenWrt libmicrohttpd feed Makefile defines both no-SSL and SSL variants in one source package. Recursively installing that feed package also follows the SSL variant's GnuTLS dependency tree; in the previous workflow this pulled in Unbound and failed because the SDK build did not stage OpenSSL.

This repository therefore carries a minimal, pinned recipe for **only** the upstream \`libmicrohttpd-no-ssl\` variant. It disables HTTPS and GnuTLS, and does not install or build the SSL sibling variant. The openNDS package recipe follows the upstream OpenWrt Makefile from the official openNDS v11.0.0 tag.

The workflow does not update or install additional package feeds.

## Build and verification

A push to \`main\` that changes a package Makefile or the workflow starts a build. A manual run is also available under **Actions → Build openNDS for OpenWrt 25.12.6 → Run workflow**.

The workflow verifies:

1. the official OpenWrt SDK SHA-256;
2. that upstream tag \`v11.0.0\` resolves to the pinned Git commit;
3. the SHA-256 of the codeload source archive;
4. that the source archive has the expected top-level directory;
5. that only \`libmicrohttpd-no-ssl\`, not the SSL/GnuTLS/Unbound packages, is selected;
6. that exactly one APK for openNDS and one APK for libmicrohttpd-no-ssl are produced.

## Artifacts

A successful run publishes:

- \`opennds_*.apk\`
- \`libmicrohttpd-no-ssl_*.apk\`
- \`SHA256SUMS\`
- \`BUILD-INFO.txt\`

Download the artifact named:

\`opennds-11.0.0-openwrt-25.12.6-mediatek-filogic\`

Do not install either APK until the successful build artifacts, package architecture, dependencies, and the router's existing package state have been checked. The workflow output is a custom build for this SDK target, not an official OpenWrt signed repository package.
