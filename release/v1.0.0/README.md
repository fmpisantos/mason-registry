# Mason Registry Release v1.0.0

This release contains the compiled mason registry for the fmpi.santos mason registry.

## Files

- `registry.json.zip` - Compiled registry containing all package definitions
- `checksums.txt` - SHA256 checksums for verification

## Packages

This release contains the following packages:

- **jdtls-17** - Java language server (v1.43.0)
- **spring-boot-tools** - Spring Boot tools for VS Code (v1.59.0)
- **vscode-java-debug-17** - Java debugging support (v0.58.0)
- **vscode-java-test-17** - Java testing support (v0.43.2)

## Usage

To use this registry with mason.nvim:

```lua
require("mason").setup({
  registries = {
    "github:fmpisantos/mason-registry@v1.0.0"
  }
})
```

## Verification

Verify the integrity of the downloaded files:

```bash
shasum -a 256 -c checksums.txt
```