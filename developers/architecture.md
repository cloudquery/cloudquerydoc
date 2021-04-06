# Architecture

This is an advanced section describing the inner workings and design of cloudquery \(might be useful when developing new providers\).

cloudquery has a pluggable architecture and is using the [go-plugin](https://github.com/hashicorp/go-plugin) to load, run and communicate between providers via gRPC. To develop a new provider for cloudquery you don’t need to understand the inner workings go-plugin as those are abstracted away [cq-provider-sdk](https://github.com/cloudquery/cq-provider-sdk).

![cloudquery high-level architecture](../.gitbook/assets/cloudquery-diagram.png)

Similarly to any application utilising the [go-plugin](https://github.com/hashicorp/go-plugin) framework, cloudquery is split into [CloudQuery Core](https://github.com/cloudquery/cloudquery) and [cloudquery providers](https://github.com/cloudquery/cloudquery/tree/main/providers).

### Cloudquery Core Responsibilities

* Main entry point and CLI for the user.
* Reading cloudquery configuration.
* Downloading, verifying and running providers.
* Running policy packs.

### Cloudquery Provider Responsibilities

* Intended to be run only by cloudquery-core.
* Communicates with cloudquery-core over gRPC to receive commands and actions.
* Initialisation, authentication and fetching data via 3rd party cloud/SaaS API

