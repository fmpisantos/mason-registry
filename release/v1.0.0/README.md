# Mason Registry Release v1.0.0

This release contains the compiled mason registry for the fmpi.santos mason registry.

## Files

- `registry.json.zip` - Compiled registry containing all package definitions
- `checksums.txt` - SHA256 checksums for verification

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