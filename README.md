# ModelMesh Serving

ModelMesh Serving is the Controller for managing ModelMesh, a general-purpose model serving management/routing layer.

## Getting Started

To quickly get started with ModelMesh Serving, check out the [Quick Start Guide](./docs/README.md).

For help, please open an issue in this repository.

## Components and their Repositories

ModelMesh Serving currently comprises components spread over a number of repositories.

![Architecture Image](./docs/architecture/images/0.2.0-highlevel.png)

Issues across all components are tracked centrally in this repo.

#### Core Components

- https://github.com/kserve/modelmesh-serving (this repo) - the model serving controller
- https://github.com/kserve/modelmesh - the ModelMesh containers used for orchestrating model placement and routing

#### Runtime Adapters

- [modelmesh-runtime-adapter](https://github.com/kserve/modelmesh-runtime-adapter) - the containers which run in each model serving pod and act as an intermediary between ModelMesh and third-party model-server containers. Its build produces a single "multi-purpose" image which can be used as an adapter to work with each of the out-of-the-box supported model servers. It also incorporates the "puller" logic which is responsible for retrieving the models from storage before handing over to the respective adapter logic to load the model (and to delete after unloading). This image is also used for a container in the load/unload path of custom `ServingRuntime` Pods, as a "standalone" puller.

#### Model Serving runtimes

ModelMesh Serving provides out-of-the-box integration with the following model servers.

- [triton-inference-server](https://github.com/triton-inference-server/server) - Nvidia's Triton Inference Server
- [seldon-mlserver](https://github.com/SeldonIO/MLServer) - Seldon's python MLServer which is part of [KFServing](https://github.com/kubeflow/kfserving)

`ServingRuntime` custom resources can be used to add support for other existing or custom-built model servers, see the docs on [implementing a custom Serving Runtime](./docs/runtimes.md)

#### Libraries

These are helper Java libraries used by the ModelMesh component.

- [kv-utils](https://github.com/IBM/kv-utils) - Useful KV store recipes abstracted over etcd and Zookeeper
- [litelinks-core](https://github.com/IBM/litelinks-core) - RPC/service discovery library based on Apache Thrift, used only for communications internal to ModelMesh.

## Contributing

Please read our [contributing guide](./CONTRIBUTING.md) for details on contributing.

### Building Images

```bash
# Build develop image
make build.develop

# After building the develop image,  build the runtime image
make build
```

test commit
