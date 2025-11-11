# Mason Registry Agent Guidelines

## Build/Lint/Test Commands

### Linting
- **YAML syntax validation**: Use `yamllint` to check YAML syntax and formatting
- **Schema validation**: Package definitions must validate against the [mason registry schema](https://github.com/mason-org/registry-schema)
- **Registry lint**: Run `mason-org/actions/registry-lint@v1` (used in CI)

### Testing
- **Local testing**: Configure mason.nvim to source packages locally:
  ```lua
  require("mason").setup {
    registries = {
      "file:~/path/to/mason-registry"
    }
  }
  ```
- **Install testing**: Use `:MasonInstall <package>` to test package installation
- **Cross-platform testing**: Use `:MasonInstall --target=<platform> <package>` to test different platforms

### Prerequisites
- Install `yq` for YAML processing: `:MasonInstall yq`
- Use YAML language server for real-time validation and autocompletion

## Code Style Guidelines

### YAML Formatting
- Use 2-space indentation
- Start documents with `---`
- Max line length: 120 characters
- Use `|` for multi-line descriptions with proper text wrapping

### Package Structure
- Files must be located at `packages/<package-name>/package.yaml`
- Follow the [package specification](https://github.com/mason-org/mason-registry/blob/main/CONTRIBUTING.md#package-specification)

### Naming Conventions
- Package names must be unique and follow the naming scheme in CONTRIBUTING.md
- Use upstream names when unambiguous
- Add clarifying prefixes/suffixes for ambiguous names
- Language-specific servers: `<language>-language-server`

### Field Requirements
- **name**: Unique, follows naming guidelines
- **description**: Sourced from upstream, split on multiple lines if long
- **homepage**: Well-formed URL (http/https), public website or source code
- **licenses**: SPDX-compatible identifiers (e.g., MIT, Apache-2.0, GPL-3.0-only)
- **languages**: Consistent casing with other packages
- **categories**: One of: Compiler, DAP, Formatter, LSP, Linter, Runtime

### Source Definition
- Must include `id` with purl-compatible identifier
- Must contain version component
- Use appropriate qualifiers for package managers (features, repository_url, etc.)

### Expressions
- Use `{{expr}}` syntax for dynamic values
- Support basic Lua syntax with transformation functions
- Common: `{{ version | strip_prefix "v" }}`

### Platform Support
- Specify `supported_platforms` when package doesn't support all platforms
- Use appropriate target identifiers (linux_x64_gnu, darwin_arm64, etc.)
- GNU binaries must use `_gnu` suffix

### Error Handling
- Validate all URLs are accessible
- Ensure all referenced files exist in packages
- Check that bin/share/opt paths are correct
- Verify expressions evaluate correctly

### Security
- Only include packages meeting the requirements (100+ stars, 5000+ downloads, etc.)
- Use proper SPDX license identifiers
- Avoid packages with proprietary licenses unless approved