# Release notes

[User guide](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/README.md) · [Polski](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/CHANGELOG.pl.md)

## 0.0.15 — 24 September 2026

- Embedded the English and Polish walkthroughs directly in the extension description, with playback controls and preview images.
- Included the new Terraform Live Values & Results name and icon. Existing Marketplace installations update under the same `bryn1u.valuescope-iac` ID.

The videos progress from simple examples to more complex configurations and show version 0.0.11 under the previous name. Calculation behavior is unchanged from 0.0.13.

## 0.0.14 — 24 September 2026

- Renamed the extension to **Terraform Live Values & Results** and added a new icon.
- Updated the name in the results panel, commands and English/Polish documentation.
- Kept `bryn1u.valuescope-iac`, settings and saved selections unchanged. Existing Marketplace installations update in place.

Calculation behavior is unchanged from 0.0.13.

## 0.0.13 — 24 September 2026

- Prepared the Marketplace release under `bryn1u.valuescope-iac`. The display name and `valuescope.*` settings are unchanged.
- Added public documentation and issue links, with links to the English and Polish walkthroughs.
- Rebuilt packages for Linux x64, Windows x64, macOS ARM64 and macOS x64.

Disable or uninstall the older local extension `valuescope.valuescope-iac` to avoid running two copies.

## 0.0.12 — 24 September 2026

This is the first public release in this repository.

- Preview variables, locals, supported expressions, configured resource arguments and local-module outputs in VS Code.
- Inspect a variable declaration from its header, type constraint or whole-block selection using the current inputs. Expressions inside `default` can be inspected separately.
- Use the English or Polish interface and choose inputs through tfvars files or profiles.
- Install a package for Linux x64, Windows x64, macOS Apple Silicon or macOS Intel. Each includes the calculation engine.

The application is free to use for personal and commercial work under the [product license](https://github.com/bryn1u/live-values-results-for-terraform/blob/main/LICENSE.txt). Third-party components retain their own licenses; each package includes the notices and the unmodified HCL source archive.

VS Code integration tests passed on Linux. Windows and macOS packages were cross-compiled and their archives checked; this release has not been run on those systems.
