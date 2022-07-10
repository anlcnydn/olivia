# WIP 

Still work in progress. 

# olivia
Olivia is a Github Action to provide automatic code generation and package publishing from an OpenApi Spec.

Code generation is performed by the action: [openapitools-generator-action](https://github.com/openapi-generators/openapitools-generator-action) and it uses the [OpenAPITools Generator](https://github.com/OpenAPITools/openapi-generator)

## Inputs

### `generator`

The generator you wish to use (i.e. the language you want to generate a client library for). See [the official list of supported languages/generators](https://openapi-generator.tech/docs/generators) and [the openapi-generator repo](https://github.com/OpenAPITools/openapi-generator) for more info.

### `config-file`

The path (with respect to the current directory/the workspace) to the config file to be used with `openapi-generator`. For information on what can be configured, see [the page on customization in the repo](https://github.com/OpenAPITools/openapi-generator/blob/master/docs/customization.md).

### `openapi-file`

The path (with respect to the current directory/the workspace) to the OpenAPI document (both JSON and YAML are supported). Defaults to "openapi.json" (i.e. a file in the current directory called openapi.json).

### `openapi-url`

The URL to load the OpenAPI document from. If set, `openapi-file` will be ignored.

### `generator-tag`

The Docker tag of the openapitools/openapi-generator-cli image to use. See [the DockerHub repo](https://hub.docker.com/r/openapitools/openapi-generator-cli/tags) for available tags.

### `template-dir`

The path (with respect to the current directory/the workspace) to the folder containing the template files. See user-defined [templates](https://openapi-generator.tech/docs/templating#modifying-templates) via options.

### `command-args`

Additional arguments to pass through to the [generate](https://openapi-generator.tech/docs/usage#generate) command.

### `output-folder`

The path which generated source codes will be placed under. By default, it will be placed under `generated` folder.

### `output-generator-type-folder-suffix`

The suffix for generated source code folders. This value will be the suffixes of generator-name under `{output-folder}`, e.g. 'generated/typescript-angular-client' if the default values used or 'generated/spring-server' if suffix passed is 'server'. 

### `keep-generated-folders`

The flag to keep or remove generated source codes. Default, true. 

## Outputs

No outputs are returned.

## Example usage
```yaml
jobs:
  generate-angular-client:
    runs-on: ubuntu-latest
    name: Example
    steps:

      # Checkout your code
      - name: Checkout
        uses: actions/checkout@v2

      # Generate your OpenAPI document (if you don't write it manually)

      # Use the action to generate a client package
      # This uses the default path for the openapi document and thus assumes there is an openapi.json in the current workspace.
      - name: Generate Angular Client
        uses: anlcnydn/olivia@v1
        with:
          generator: typescript-angular
          config-file: angular-generator-config.yml
          output-folder: output

```

## Template example usage
```yaml
jobs:
  generate-angular-client:
    runs-on: ubuntu-latest
    name: Example
    steps:

      # Checkout your code
      - name: Checkout
        uses: actions/checkout@v2

      # Generate your OpenAPI document (if you don't write it manually)

      # Use the action to generate a client package
      # This uses the default path for the openapi document and thus assumes there is an openapi.json in the current workspace.
      - name: Generate Angular Client
        uses: anlcnydn/olivia@v1
        with:
          generator: typescript-angular
          config-file: angular-generator-config.yml
          template-dir: templates/typescript-angular

```