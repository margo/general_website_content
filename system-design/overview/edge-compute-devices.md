# Compute Target

A Compute Target is the compute Margo workloads are deployed to and run on. It is provided by compute hardware present in the customer's environment, which is what lets workloads run locally within the industrial environment, close to the devices, databases, and other critical control system entities they interact with. Running compute at the edge keeps latency low, keeps operations resilient when connectivity is intermittent, and keeps sensitive data on-site.

A Compute Target is defined by what it can offer a workload rather than by the hardware behind it. It reports the deployment types and runtimes it supports, along with the CPU, memory, storage, peripherals, and network interfaces available to Margo, and a workload fleet manager uses that information to decide which workloads it can host.

## How Compute Targets are provided

The same deployment model applies no matter what sits underneath, which means a fleet manager treats each of these the same way:

- A single edge compute device hosting its own management client
- A multi-node cluster presented through one management client
- Devices that cannot host a management client of their own, connected through a [gateway service](../concepts/gateways/gateways.md)

Because a Compute Target can span several pieces of hardware, it does not necessarily map one to one onto a physical device.

## Benefits for compute suppliers

The Margo specification provides [compute suppliers](../personas-and-definitions/personas.md#compute-supplier) the following benefits:

- A Margo compliant Compute Target works with any Margo compliant workload fleet manager, so the integration work is done once rather than repeated for each fleet manager an end user might choose.
- Suppliers keep freedom of choice over the components they implement, such as supported manifests, container orchestration platforms, and workload runtimes.
- Existing hardware that cannot host a management client can still take part in the ecosystem through a gateway service, which avoids redesigning a product line to make it Margo compliant.

## Margo device layers

Margo devices consist of three major layers: Margo interface layer, platform layer, and traditional device layer. Although Margo requires compliance towards its requirements, such as hosting the Margo management interface client, the compute supplier has freedom to implement as they see fit.

Below is a diagram that depicts the device layers along with some examples:

![Device Layer Drawing)](../figures/device-layers.drawio.svg)

## Relevant Links

Please follow the subsequent links to view more technical information regarding Compute Targets and Margo compliant devices:

- [Compute Target Concepts](../concepts/edge-compute-devices/devices.md)
- [Gateway Services](../concepts/gateways/gateways.md)
- [Collecting Application Observability Data](../specification/observability/collecting-workload-observability-data.md)
