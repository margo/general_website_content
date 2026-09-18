# Technical Lexicon

Below are concepts and terms utilized throughout the Margo Specification along with their associated description/definition.

## Concepts

#### Interoperability

Interoperability is an overloaded term that has different meanings depending on the context. For Margo, interoperability is about achieving the following:

- Defining a common approach for packaging [Components](#component) so they can be deployed as [Workloads](#workload) to any compatible Margo-compliant [Compute Target](#compute-target) via any Margo-compliant [Workload Fleet Manager](#workload-fleet-manager).
- Defining a common API to enable communication between any Margo-compliant [Compute Target](#compute-target) and any Margo-compliant [fleet management](#fleet-management) software.
- Defining a common approach for collecting and transmitting diagnostics and observability data from a Margo-compliant [Compute Target](#compute-target)

#### Orchestration

Orchestration is an overloaded term that has different meanings depending on the context. For Margo, orchestration is the deployment of [Workloads](#workload) to Margo-compliant [Compute Targets](#compute-target). A [Workload Fleet Manager](#workload-fleet-manager) describes what should run as a deployment specification, and the [Provider services](#provider-model) running on the Compute Target apply that specification to the local container orchestration platform.

Margo depends on container orchestration platforms such as Kubernetes, Docker and Podman already existing on the Compute Target and is not an attempt to duplicate what these platforms provide.

#### Fleet Management

Fleet Management represents a concept or pattern that enables users to manage one to many set of [workloads](#workload) the customer owns. Many strategies exist within fleet management such as canary deployments, rolling deployments, and many others. Below are two fleet management concepts that have been adopted by Margo.

##### State Seeking

The state seeking methodology, adopted via Margo, is enabled first by the [Workload Fleet Manager](#workload-fleet-manager) when it establishes the "Desired state". The client managing the [Compute Target](#compute-target) then reconciles its "Current state" with the "Desired state" provided by the Fleet Manager and reports the status.

##### Provider Model

The provider model within Margo describes a service, running alongside the [Workload Fleet Management Client](#workload-fleet-management-client) on the [Compute Target](#compute-target), that takes the deployment specifications from the desired state and applies them to the local container orchestration platform. Each deployment type has its own provider, which is how Margo supports more than one packaging format without the [Workload Fleet Manager](#workload-fleet-manager) needing to understand each one.
Current providers supported:

- Helm Client
- Compose Client

## Technical Terms

#### Application

An application is a collection of one, or more, [Components](#component), as defined by an [Application Description](../specification/applications/application-description.md), and bundled within an [Application Package](#application-package).

#### Application Package

An Application Package is used to distribute an [application](#application). The parts of an Application Package are: Application Description (that refers to contained and deployable Components) as well as associated resources (e.g., icons). While the application package is made available in an [Application Registry](../concepts/applications/application-registry.md), the referenced [components](#component) are stored in a [Component Registry](#component-registry), and the linked containers are provided via a OCI [Container Image Registry](#container-image-registry).

#### Component

A Component is a piece of software tailored to be deployed within a customer's environment on a [Compute Target](#compute-target).
Currently Margo-supported components are:

- Helm Chart
- [Compose Archive](#compose-archive)

#### Compose Archive
A Compose Archive is a tarball file containing the Compose file, `compose.yaml`, which is formatted according the [Compose specification](https://www.compose-spec.io/), and any additional artifacts referenced by the Compose file (e.g., configuration files, environment variable files, etc.). 

#### Workload

A Workload is an instance of a [Component](#component) running within a customer's environment on a [Compute Target](#compute-target).

#### Compute Target

A Compute Target is the logical compute that Margo [Workloads](#workload) are deployed to and run on. It reports the deployment types, runtimes, compute resources, peripherals, and network interfaces it makes available to Margo, and a [Workload Fleet Manager](#workload-fleet-manager) uses that information to decide which workloads it can host.

A Compute Target is a logical concept rather than a physical one. A single [Edge Compute Device](#edge-compute-device) may present one Compute Target, and a [Gateway Service](#gateway-service) may present several downstream devices as separate Compute Targets or combine them into one.

#### Target Name

A Target Name is the human assigned name given to a [Compute Target](#compute-target) so operators can recognize it and select it when deploying workloads. It is a label chosen by people, not a generated identifier, and it carries no security meaning. Component identity used for authentication comes from the [Margo Identity and Authorization Framework](../concepts/identity/identity-and-trust.md) instead.

#### Edge Compute Device

Edge Compute Devices are represented by compute hardware that runs within the customer's environment to enable the system with Margo Compliant [Workloads](#workload). Edge Compute Devices host the Margo compliant WFM Client, container orchestration platform, and device operating systems. An Edge Compute Device or devices provides the [Compute Target](#compute-target) that workloads are deployed to, either directly or through a [Gateway Service](#gateway-service).

#### Gateway Service

A [Gateway Service](../concepts/gateways/gateways.md) connects devices that do not host a Margo management client of their own, translating between those devices and a [Workload Fleet Manager](#workload-fleet-manager) so they can still provide a [Compute Target](#compute-target). The service may run on a server, within a device, or on hardware dedicated to it, which is commonly called a gateway device.

#### Workload Fleet Manager

Workload Fleet Manager (WFM) represents a software offering that enables End Users to configure, deploy, and manage edge [Workloads](#workload) as a fleet across their registered [Compute Targets](#compute-target).

##### Workload Fleet Management Client

The Workload Fleet Management client is a service that runs on the edge compute which communicates with the [Workload Fleet Manager](#workload-fleet-manager) to receive [Components](#component) that will be instantiated as [Workloads](#workload) and configurations to be applied to the [Compute Target](#compute-target) it manages.

#### Device Fleet Manager

Device Fleet Manager (DFM) represents a software offering that enables End Users to onboard, delete, and maintain [Edge Compute Devices](#edge-compute-device) within the ecosystem. This software is utilized in conjunction with the [Workload Fleet Manager](#workload-fleet-manager) software to provide users with the features required to manage their [Edge Device](#edge-compute-device) along with [Workloads](#workload) running on them.  

> Note: The Device Fleet Manager is a future component of the Margo specification. This section will be expanded as the community defines device management functionality. 


#### Application Registry

An [Application Registry](../concepts/applications/application-registry.md) hosts [Application Packages](#application-package) that define, through their [Application Description](../specification/applications/application-description.md), the application as one or multiple [Components](#component).
It is used by application developers to make their applications available.
The [API of the Application Registry](../specification/applications/application-registry.md) is compliant with the [OCI Registry API (v1.1.0)](https://github.com/opencontainers/distribution-spec/blob/v1.1.0/spec.md).


#### Application Catalog

An Application Catalog is a visual representation of preselected, install-ready applications, the user of the [WFM](#workload-fleet-manager) can deploy to its managed [Compute Targets](#compute-target). Application Catalogs and how they function within the WFM are out of scope for Margo.


#### Component Registry

A Component Registry holds [Components](#component) (e.g., Helm Charts and Compose Archives) for [Application Packages](#application-package).
When an application gets deployed through a [Workload Fleet Manager](#workload-fleet-manager), the components (linked within an [Application Description](../specification/applications/application-description.md)) are requested from the Component Registry and then deployed as [workloads](#workload). Components link to containers that are typically provided through [Container Registries](#container-image-registry).
The Component Registry can be implemented, e.g., as an OCI Registry.

#### Container Image Registry
A Container Image Registry hosts container images. [Components](#component) which are provided  as Helm Charts or Compose Archives link to such container images.

## Identity Terms

The following terms belong to the [Margo Identity and Authorization Framework](../specification/identity/identity-framework.md) (MIAF), Margo's common foundation for identity, authentication, and authorization. MIAF builds on the open [SPIFFE](https://spiffe.io/) standard. The entries below are informative summaries; the authoritative definitions are in the [MIAF terminology](../specification/identity/identity-framework.md#terminology).

#### Trust Domain

A governed security boundary within which identities are issued and mutually recognized: it defines the trust anchors, the identity namespace, and the policies that govern them. Defined in the [MIAF terminology](../specification/identity/identity-framework.md#terminology).

#### SPIFFE ID

A URI of the form `spiffe://<trust-domain>/<path>` that names an identity within a [Trust Domain](#trust-domain). Defined in the [MIAF terminology](../specification/identity/identity-framework.md#terminology).

#### SVID

A SPIFFE Verifiable Identity Document: the verifiable credential representing an identity within a [Trust Domain](#trust-domain), which a component presents when it authenticates over mutual TLS. Defined in the [MIAF terminology](../specification/identity/identity-framework.md#terminology).

#### Trust Bundle

The set of X.509 trust anchors a [Trust Domain](#trust-domain) publishes so that verifiers can validate [SVIDs](#svid) issued within the domain. Defined in the [MIAF terminology](../specification/identity/identity-framework.md#terminology).

#### Margo Identity Service

The identity-authority role within a [Trust Domain](#trust-domain), abbreviated MIS: it issues [SVIDs](#svid) and publishes the [Trust Bundle](#trust-bundle) and discovery document, and is defined by these responsibilities rather than by a specific product. Defined in the [MIAF terminology](../specification/identity/identity-framework.md#terminology).

#### Principal

A non-human Margo component that holds, or is being provisioned with, an identity in a [Trust Domain](#trust-domain); an [Edge Compute Device](#edge-compute-device) participates through the WFM Client it hosts. Defined in the [MIAF terminology](../specification/identity/identity-framework.md#terminology).

#### WFM Identity

The identity of a [Workload Fleet Manager](#workload-fleet-manager) within its [Trust Domain](#trust-domain). It anchors the namespace under which that WFM's client identities are issued. The naming rules are in the [WFM Identity Profile](../specification/identity/wfm-identity-profile.md).

#### WFM Client Identity

The identity of a WFM Client relationship within a [Trust Domain](#trust-domain), named under the [WFM](#wfm-identity) that issues it. The naming rules are in the [WFM Identity Profile](../specification/identity/wfm-identity-profile.md).
