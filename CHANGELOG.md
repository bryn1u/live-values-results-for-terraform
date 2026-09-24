# Release notes

[User guide](README.md) · [Polski](CHANGELOG.pl.md)

## 0.0.12 — 24 September 2026

This is the first public release in this repository.

- Preview variables, locals, supported expressions, configured resource arguments and local-module outputs in VS Code.
- Inspect a variable declaration from its header, type constraint or whole-block selection using the current inputs. Expressions inside `default` can be inspected separately.
- Use the English or Polish interface and choose inputs through tfvars files or profiles.
- Install a package for Linux x64, Windows x64, macOS Apple Silicon or macOS Intel. Each includes the calculation engine.

The application is free to use for personal and commercial work under the [product license](LICENSE.txt). Third-party components retain their own licenses; each package includes the notices and the unmodified HCL source archive.

VS Code integration tests passed on Linux. Windows and macOS packages were cross-compiled and their archives checked; this release has not been run on those systems.
