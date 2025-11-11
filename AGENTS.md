# Mason Registry Agent Guidelines

## Build/Lint/Test Commands
- **Lint**: `yamllint packages/*/package.yaml` for YAML syntax; use `mason-org/actions/registry-lint@v1` for schema validation
- **Test single package**: Configure mason locally with `registries = {"file:~/path/to/mason-registry"}`, then `:MasonInstall <package>`
- **Cross-platform test**: `:MasonInstall --target=<platform> <package>` (e.g., linux_x64_gnu, darwin_arm64)
- **Prerequisites**: Install `yq` via `:MasonInstall yq` for YAML processing

## Code Style Guidelines
- **YAML formatting**: 2-space indent, start with `---`, max 120 chars/line, use `|` for multi-line descriptions
- **Package structure**: Place in `packages/<name>/package.yaml`; follow [package spec](https://github.com/mason-org/mason-registry/blob/main/CONTRIBUTING.md#package-specification)
- **Naming**: Unique names following CONTRIBUTING.md; use upstream names, add prefixes/suffixes for clarity; `<language>-language-server` for LSPs
- **Required fields**: name, description (from upstream), homepage (valid URL), licenses (SPDX), languages, categories (Compiler|DAP|Formatter|LSP|Linter|Runtime)
- **Source**: Include `id` with purl-compatible identifier and version; use qualifiers for package managers
- **Expressions**: Use `{{expr}}` for dynamic values with Lua syntax; common: `{{ version | strip_prefix "v" }}`
- **Platform support**: Specify `supported_platforms` if not universal; use correct target IDs; GNU binaries need `_gnu` suffix
- **Error handling**: Validate URLs, verify file paths exist, check bin/share/opt paths, test expressions
- **Security**: Only approved packages (100+ stars, 5000+ downloads); use proper SPDX licenses; avoid proprietary unless approved