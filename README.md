
[![Build Status](https://travis-ci.org/nginxinc/kubernetes-ingress.svg?branch=master)](https://travis-ci.org/nginxinc/kubernetes-ingress)  [![FOSSA Status](https://app.fossa.io/api/projects/custom%2B1062%2Fgithub.com%2Fnginxinc%2Fkubernetes-ingress.svg?type=shield)](https://app.fossa.io/projects/custom%2B1062%2Fgithub.com%2Fnginxinc%2Fkubernetes-ingress?ref=badge_shield)  [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)  [![Go Report Card](https://goreportcard.com/badge/github.com/nginxinc/kubernetes-ingress)](https://goreportcard.com/report/github.com/nginxinc/kubernetes-ingress)

# NGINX Ingress Controller

This repo provides an implementation of an Ingress controller for NGINX and NGINX Plus.

**Note**: this project is different from the NGINX Ingress controller in [kubernetes/ingress-nginx](https://github.com/kubernetes/ingress-nginx) repo. See [this doc](docs/nginx-ingress-controllers.md) to find out about the key differences.


## NGINX+ Ingress Controller with App Protect WAF module

NGINX Ingress controller works with both NGINX and NGINX Plus and supports the standard Ingress features - content-based routing and TLS/SSL termination.

**App Protect WAF module currenly only supports NGINX Plus**

Additionally, several NGINX and NGINX Plus features are available as extensions to the Ingress resource via annotations and the ConfigMap resource. In addition to HTTP, NGINX Ingress controller supports load balancing Websocket, gRPC, TCP and UDP applications. See [ConfigMap and Annotations doc](docs/configmap-and-annotations.md) to learn more about the supported features and customization options.

As an alternative to the Ingress, NGINX Ingress controller supports the VirtualServer and VirtualServerRoute resources. They enable use cases not supported with the Ingress resource, such as traffic splitting and advanced content-based routing. See [VirtualServer and VirtualServerRoute Resources doc](docs/virtualserver-and-virtualserverroute.md).

Read [this doc](docs/nginx-plus.md) to learn more about NGINX Ingress controller with NGINX Plus.

NGINX Plus App Protect module has been added to provide an industry-leading WAF service for k8s workloads fronted by NGINX. See below for instructions on how to build NGINX+ with App Protect module

## Getting Started

1. Install the NGINX Ingress controller using the Kubernetes [manifests](deployments) or the [helm chart](deployments/helm-chart).
1. Configure load balancing for a simple web application:
    * Use the Ingress resource. See the [Cafe example](examples/complete-example).
    * Or the VirtualServer resource. See the [Basic configuration](examples-of-custom-resources/basic-configuration) example.
1. See additional configuration [examples](examples).
1. Learn more about all available configuration and customization in the [docs](docs).


## NGINX Ingress Controller Releases

We publish Ingress controller releases on GitHub. See our [releases page](https://github.com/nginxinc/kubernetes-ingress/releases).

The latest stable release is [1.6.0](https://github.com/nginxinc/kubernetes-ingress/releases/tag/v1.6.0). For production use, we recommend that you choose the latest stable release.  As an alternative, you can choose the *edge* version built from the [latest commit](https://github.com/nginxinc/kubernetes-ingress/commits/master) from the master branch. The edge version is useful for experimenting with new features that are not yet published in a stable release.

To use the Ingress controller, you need to have access to:
* An Ingress controller image.
* Installation manifests or a Helm chart.
* Documentation and examples.

It is important that the versions of those things above match.

The table below summarizes the options regarding the images, manifests, helm chart, documentation and examples and gives your links to the correct versions:

| Version | Description |  Image for NGINX | Image for NGINX Plus | Installation Manifests and Helm Chart | Documentation and Examples |
| ------- | ----------- | --------------- | -------------------- | ---------------------------------------| -------------------------- |
| Latest stable release | For production use | `nginx/nginx-ingress:1.6.0`, `nginx/nginx-ingress:1.6.0-alpine` from [DockerHub](https://hub.docker.com/r/nginx/nginx-ingress/) or [build your own image](https://github.com/nginxinc/kubernetes-ingress/tree/v1.6.0/build). | [Build your own image](https://github.com/nginxinc/kubernetes-ingress/tree/v1.6.0/build). | [Manifests](https://github.com/nginxinc/kubernetes-ingress/tree/v1.6.0/deployments). [Helm chart](https://github.com/nginxinc/kubernetes-ingress/tree/v1.6.0/deployments/helm-chart). | [Documentation](https://github.com/nginxinc/kubernetes-ingress/tree/v1.6.0/docs). [Examples](https://github.com/nginxinc/kubernetes-ingress/tree/v1.6.0/examples). |
| Edge | For testing and experimenting | `nginx/nginx-ingress:edge`, `nginx/nginx-ingress:edge-alpine` from [DockerHub](https://hub.docker.com/r/nginx/nginx-ingress/) or [build your own image](https://github.com/nginxinc/kubernetes-ingress/tree/master/build). | [Build your own image](https://github.com/nginxinc/kubernetes-ingress/tree/master/build). | [Manifests](https://github.com/nginxinc/kubernetes-ingress/tree/master/deployments). [Helm chart](https://github.com/nginxinc/kubernetes-ingress/tree/master/deployments/helm-chart). | [Documentation](https://github.com/nginxinc/kubernetes-ingress/tree/master/docs). [Examples](https://github.com/nginxinc/kubernetes-ingress/tree/master/examples). |

## Building NGINX+ with App Protect module

1. Clone this repo
2. Copy "app-protect-<release>.zip" to the repo folder
3. Run the following:
  `make DOCKERFILE=Dockerfile PREFIX=<repo_name>/<container_name> GENERATE_DEFAULT_CERT_AND_KEY=1 RELEASE=20`
4. Process will push the container to selected *PRIVATE* repo

## Support

For NGINX Plus customers NGINX Ingress controller (when used with NGINX Plus) is covered
by the support contract.
