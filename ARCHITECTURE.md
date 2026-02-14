# kontakt-android-sdk — Architecture

## Overview
This repository serves as the public distribution archive for the Kontakt.io Android SDK. It contains pre-built SDK JAR/AAR artifacts across multiple major versions (4.x through 7.x), published for external developer consumption. It is not a source code repository but rather a release artifact store used to distribute the SDK binary to third-party developers. The latest version is 7.0.12.2.

## Status
Stale — last commit 2023-01-17. This repository appears to be a static artifact archive that is no longer actively updated. The SDK source is maintained in the `android-sdk` repository instead.

## Tech Stack
- Pre-built Android SDK artifacts (JAR/AAR)
- No build system present (no build.gradle files)
- Distribution format: Binary archive

## Components / Modules
- **Archive/** — Contains historical SDK versions organized by version number:
  - Versions 4.0.0 through 7.0.12.2
  - Each version directory contains the compiled SDK artifact
- **7.0.12.2/** — Root-level directory for the latest SDK JAR (`android_sdk_7.0.12.2.jar`)

## Interfaces
- **Exposes:**
  - Kontakt.io Android SDK binary artifacts for integration into third-party Android apps
  - Maven coordinate (historical): `io.kontakt.mvn:sdk:{version}`
- **Consumes:** None (binary distribution only)
- **Data Stores:** None

## Architecture Notes
- This is a distribution-only repository; no source code is present.
- The actual SDK source code is maintained in the `android-sdk` repository.
- Contains 23 files total, primarily versioned artifact directories.
- The README references public documentation at Stoplight for developer integration guides.

## Known Issues / Risks
- Repository has not been updated since January 2023, meaning newer SDK versions (if any exist beyond 7.0.12.2) are not distributed here.
- If external developers depend on this repo for SDK updates, they may not receive the latest fixes.
- Contains only 23 files suggesting minimal structure; no CI/CD or automated publishing pipeline is visible.
- The distribution model (git repo as artifact store) is unusual; Maven Central or a private Maven repository would be more conventional.
