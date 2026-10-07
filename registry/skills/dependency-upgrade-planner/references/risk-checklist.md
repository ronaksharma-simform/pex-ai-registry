# Risk checklist

Use this to place each outdated package in a group.

## Low risk
- Patch version bump (`1.4.2` to `1.4.3`).
- Minor version bump of a package that follows semantic versioning and has a changelog.
- Dev-only tools that do not ship to production (linters, formatters).

## Medium risk
- Minor bump of a package with a history of behaviour changes in minor releases.
- A package that other packages in the project depend on.
- Any change to the build tool or the test runner.

## High risk
- Major version bump.
- A framework or runtime (the language version, the web framework, the ORM).
- A package with no changelog or no tests in your project covering it.

## Always first
- Any bump that fixes a published security advisory, whatever its version size.

## Before each step
- Read the package's release notes for the versions in between.
- Run the full test suite on a clean install of the lockfile.
