# fabric-proto

Wire contracts for the Telaron Fabric control plane — protobuf definitions and
generated Go for the gateway ↔ control-plane API.

This module is the single source of truth for the contract between the FOSS
gateway appliance (client) and the Telaron platform (server). Both sides import
the generated Go; neither depends on the other's codebase.

## Layout

```
proto/telaron/control/v1/   protobuf sources (buf module root: proto/)
gen/go/                     generated Go (committed; kept in sync by CI)
```

## Consuming

```
go get github.com/telaron-labs/fabric-proto
```

```go
import controlv1 "github.com/telaron-labs/fabric-proto/gen/go/telaron/control/v1"
```

## Developing

Requires [buf](https://buf.build) plus `protoc-gen-go` and `protoc-gen-go-grpc`
on PATH.

```sh
buf lint
buf generate        # regenerate gen/go — commit the result
buf breaking --against '.git#branch=main'
```

CI enforces lint, breaking-change checks against `main`, and that `gen/go`
matches the proto sources.

## Versioning

Packages are versioned in the path (`telaron.control.v1`). Breaking changes
require a new version package, never an in-place edit — `buf breaking` gates
this on every PR.

## Licence

Apache 2.0 — see [LICENSE](LICENSE).
