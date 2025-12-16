# Verbio Speech Center Protobuf definition #

This repository contains the definitions of the protobuf files to enable the communication between the public gRCP
service and the client.

## How to use

We recommend generating the code using the [buf](https://buf.build/home) tool. Also, there are many other options to
generate the code, including the official protoc plugin.

### Generate Go code with Buf

Below is a minimal end‑to‑end example that generates Go stubs from the protobufs in this repository using buf’s
managed plugins. It does not require any additional configuration files in the repo.

#### Prerequisites:
- Go 1.20+ installed
- buf installed (see https://buf.build/docs/installation)

#### Steps:
1) From the root of this repository, create a `buf.gen.yaml` template (you can delete it after generation). 
   Replace `example.com/your/module` with your Go module path if you intend to import the generated code from
   another module.

```yaml
version: v2
managed:
  enabled: true
  # buf will inject missing go_package options using this prefix so modern
  # protoc-gen-go works even though the protos don’t declare go_package.
  go_package_prefix:
    default: example.com/your/module/gen/go
plugins:
  - plugin: buf.build/protocolbuffers/go
    out: gen/go
    opt: paths=source_relative
  - plugin: buf.build/grpc/go
    out: gen/go
    opt: paths=source_relative
```

2) Generate the Go code to `./gen/go` by pointing buf at the `proto` directory in this repo:

```
buf generate https://github.com/verbio-technologies/public-grpc-protos.git#tag=1.0.0,subdir=proto
```

This will create Go files under `gen/go/speechcenter/recognizer/v1/` for:
- `recognition.proto` (service + common types)
- `recognition_streaming_request.proto`
- `recognition_streaming_response.proto`

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available,
see the [tags on this repository](https://github.com/verbio-technologies/public-grpc-protos/tags).

## Licence

Check the [LICENCE](./LICENSE) file.
