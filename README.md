# Mason Registry

A personal mason registry for Neovim package management.

## Packages

This registry contains the following packages:

- **jdtls** - Java language server
- **lombok-nightly** - Lombok nightly builds
- **openjdk-17** - OpenJDK 17 runtime
- **spring-boot-tools** - Spring Boot tools for VS Code
- **vscode-java-debug** - Java debugging support
- **vscode-java-test** - Java testing support

## Usage

### Local Development

Configure mason to use this registry locally:

```lua
require("mason").setup({
  registries = {
    "file:~/path/to/mason-registry"
  }
})
```

### Production Usage

Once published to GitHub, users can consume this registry:

```lua
require("mason").setup({
  registries = {
    "github:fmpisantos/mason-registry@v1.0.0"
  }
})
```

## Development

### Adding Packages

1. Create a new directory under `packages/`
2. Add a `package.yaml` file following the [package specification](https://github.com/mason-org/mason-registry/blob/main/CONTRIBUTING.md#package-specification)
3. Test locally using the file registry method
4. Commit and create a new release

### Creating Releases

Releases are automatically created via GitHub Actions when you:

1. Push a new tag: `git tag v1.0.1 && git push origin v1.0.1`
2. Or manually trigger the workflow with a custom tag name

The release will contain:
- `registry.json.zip` - Compiled registry
- `checksums.txt` - SHA256 checksums

## Contributing

See [AGENTS.md](AGENTS.md) for coding guidelines and development setup.