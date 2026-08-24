# Dependencies and software supply chain

Treat every third-party package, plugin, action, image and tool as code that enters the project's trust boundary.

Do not add, upgrade, downgrade or replace a dependency merely because it is familiar, popular or suggested by a model. Dependency facts and security status change over time and must be verified at the time of the decision.

## Justify the dependency first

Before introducing a dependency:

1. Confirm that the standard library, platform or an existing project dependency does not already solve the problem safely.
2. State the concrete capability the dependency provides.
3. Prefer the smallest dependency with the narrowest required scope.
4. Consider the long-term cost: updates, vulnerabilities, licensing, build time, bundle size and operational ownership.
5. Distinguish a development-only tool from code that will run in production.

Do not add a package to avoid writing a small, clear and well-tested operation when the package creates more risk or maintenance than it removes.

## Verify the package and exact version

Use current online sources and the project's approved tooling. Do not rely on model memory for time-sensitive package facts.

Verify at least:

- exact package name, namespace, registry and publisher or maintainer
- official registry and source repository, watching for typosquatting or a misleading fork
- known vulnerabilities, malware reports and security advisories for the package and the exact proposed version
- whether the release is supported, maintained or end-of-life
- release history, recent ownership changes and other maintenance or provenance warning signs
- direct and transitive dependencies, including unexpected additions
- install, post-install, build or generation scripts that execute code
- requested permissions, native binaries, network access or runtime capabilities
- license and compatibility with the project and its distribution model
- compatibility with the exact runtime, language, framework, operating system, deployment target and relevant existing dependencies
- release notes, breaking changes, peer constraints and required migrations

Popularity, download counts, a clean package description or the absence of a known advisory is not proof that a package is safe.

Prefer authoritative sources such as official registries, maintainer documentation, release notes, ecosystem security advisories and the project's configured security scanner. Corroborate material uncertainty instead of trusting a single search result.

If current verification is impossible, state what could not be checked. Do not describe the dependency or version as verified, secure or compatible.

## Introduce or change a dependency safely

- Use the project's existing package manager and approved registries.
- Preserve registry integrity and signature or checksum verification where the ecosystem supports it.
- Use the package manager to update both the manifest and lockfile; do not hand-edit generated lock data.
- Follow the project's version-pinning policy and commit the lockfile when the project uses one.
- Avoid unrelated bulk upgrades when one dependency is being changed.
- Inspect the complete manifest and lockfile diff, including changed transitive dependencies.
- Do not run unreviewed remote installation commands or pipe downloaded scripts directly into a shell.
- Run the relevant dependency audit or vulnerability scanner, while recognizing that scanners do not prove safety.
- Build and test the affected deliverables against the project's actual supported runtime matrix.
- Record the reason, selected version and material compatibility or security findings when the choice is consequential.
- Keep the change easy to revert and document required migration or rollback steps.

Pause for human review when organizational policy requires approval, a package has unclear provenance, a critical advisory is unresolved, the license is uncertain or compatibility cannot be demonstrated safely.

## Upgrades are new decisions

An existing dependency is not automatically safe to upgrade.

For an upgrade:

1. Re-check the exact target version and current advisories.
2. Review breaking changes, migrations and changed transitive dependencies.
3. Confirm runtime and ecosystem compatibility again.
4. Run focused regression tests plus the broader affected build and test suite.
5. Verify deployment and rollback implications separately from local success.

Maintain an inventory or software bill of materials when required by the project's risk level or organizational policy. Remove dependencies that are unused, unsupported or no longer justify their risk.
