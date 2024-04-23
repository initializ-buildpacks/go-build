# Go Build Cloud Native Buildpack

The Go Build CNB handles the `go build` compilation process for Go programs, transforming source code in the application directory into an executable. This executable is then set as the start command for the resulting image.

## Integration

The Go Build CNB doesn't directly provide any dependencies. However, to execute the `go build` compilation process, it relies on the `go` dependency, typically supplied by a buildpack like the [Go Distribution CNB](https://github.com/initializ-buildpacks/go-dist).

## Usage

To package this buildpack for distribution:

```
$ ./scripts/package.sh
```

By default, the script packages the buildpack's Go source using `GOOS=linux`. You can specify another value as the first argument to `package.sh`.

## Go Build Configuration

Please set the following environment variables at build time, either directly (e.g., `pack build my-app --env BP_ENVIRONMENT_VARIABLE=some-value`) or through a [`project.toml` file](https://github.com/buildpacks/spec/blob/main/extensions/project-descriptor.md).

### `BP_GO_BUILD_LDFLAGS`

The `BP_GO_BUILD_LDFLAGS` variable allows you to specify values for the `-ldflags` build flag during program compilation.

```shell
BP_GO_BUILD_LDFLAGS= -X main.variable=some-value
```


### `BP_GO_TARGETS`
The BP_GO_TARGETS variable enables you to specify multiple programs for compilation. The first target will serve as the start command for the resulting image.
```shell
BP_GO_TARGETS=./cmd/web-server:./cmd/debug-server
```