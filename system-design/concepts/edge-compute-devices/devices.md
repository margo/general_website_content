# Devices

Margo devices are defined by the capabilities they provide to the Margo ecosystem. When a device onboards with a workload fleet manager, it reports what it can do, and the fleet manager uses that information to decide which workloads the device can host. Reported capabilities fall into the following categories.

## Supported Deployment Types

This describes the type of workload manifests the device can interpret and apply to its local workload runtime. Common examples are Helm and Compose manifests. A device may support more than one deployment type, giving the fleet manager flexibility in how workloads are packaged and delivered.

## Supported Runtimes

This describes the workload runtime available on the device to execute deployed workloads. Margo currently supports the OCI runtime, with additional runtimes expected in the future. As with deployment types, a device may report more than one runtime.

## Compute Resources

To ensure a device can host the workloads assigned to it, each Margo device reports the compute resources it makes available to Margo, including CPU, memory, and storage, along with peripherals and network interfaces. These resources are reported during the final stage of onboarding and updated whenever a change occurs on the device, so the fleet manager can always match workload requirements against real, available capacity.

## Gateway Devices

Gateway devices add flexibility at the edge compute layer by connecting devices that do not host a Margo management client of their own. A gateway can act as an **opaque gateway**, which combines the capabilities of several child devices and presents them to the fleet manager as a single device, or as a **see-thru gateway**, which reports each child device individually so the fleet manager can see and target them as distinct devices. For the full description of gateway behavior, see [Gateways](../gateways/gateways.md).




