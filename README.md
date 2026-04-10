# fastbit-ci-tools

Reusable GitHub Actions for Fastbit embedded firmware CI pipelines. Centralises tool installation so all projects use the same pinned versions.

## Actions

### setup-arm-gcc

Downloads and caches the ARM GNU toolchain for cross-compiling Cortex-M firmware.

```yaml
- uses: FASTBIT-EMBEDDED/fastbit-ci-tools/setup-arm-gcc@v1
```

| Input | Default | Description |
|-------|---------|-------------|
| `version` | `14.2.rel1` | ARM GNU toolchain release tag |

First run downloads the tarball (~150 MB). Subsequent runs restore from cache in seconds.

### setup-static-analysis

Installs cppcheck, clang-tidy, and clang-format with a pinned LLVM version.

```yaml
- uses: FASTBIT-EMBEDDED/fastbit-ci-tools/setup-static-analysis@v1
```

| Input | Default | Description |
|-------|---------|-------------|
| `clang-version` | `18` | LLVM major version |

### setup-coverage

Installs lcov and genhtml for test coverage reporting.

```yaml
- uses: FASTBIT-EMBEDDED/fastbit-ci-tools/setup-coverage@v1
```

No inputs required.

## Versioning

Projects reference actions with `@v1`. The `v1` tag is moved forward for non-breaking updates (tool version bumps, bug fixes). Breaking changes bump to `@v2`.

## Maintenance

To update a tool version:

1. Edit the relevant `action.yml`
2. Commit and push to `main`
3. Move the tag: `git tag -fa v1 -m "Update description" && git push --force origin v1`
4. All consumer projects pick up the change on their next CI run

## Tool versions (v1)

| Tool | Version | Source |
|------|---------|--------|
| ARM GNU toolchain | 14.2.rel1 | developer.arm.com tarball |
| clang-tidy | 18.x | LLVM apt repo |
| clang-format | 18.x | LLVM apt repo |
| cppcheck | system (apt) | Ubuntu apt |
| lcov | system (apt) | Ubuntu apt |
