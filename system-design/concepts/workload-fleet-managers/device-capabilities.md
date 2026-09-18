# Compute Target Capabilities

The purpose of capability reporting is to ensure the Workload Fleet Management (WFM) solution has the information needed to pair workloads with compatible Compute Targets. Capabilities are reported to the WFM web service using the [Device Capabilities API](../../specification/margo-management-interface/device-capabilities.md).

**Note:** _Only the capabilities that are explicitly exposed and accessible to Margo workloads are reported. If a device feature is isolated from the Margo runtime environment, it is excluded from the capabilities report. For example, an onboard camera used exclusively for local device security—and completely isolated from Margo—is not reported as an available capability. This ensures workloads are not scheduled against unavailable or restricted hardware resources._

### Capability Reporting

Capabilities and characteristics are reported when the client first connects to the Workload Fleet Management solution. Additionally, during the lifecycle of the Compute Target, if there is a change that impacts the reported characteristics, the client updates the Workload Fleet Manager with the latest information via the [Device Capabilities API](../../specification/margo-management-interface/device-capabilities.md).

A workload hosting Compute Target exchanges the following information:

- Target Name, the human assigned name operators use to recognize and select it
- Resources available for workloads to utilize:
    - CPU information
    - Memory Capacity
    - Storage Capacity
- Peripherals (e.g., graphics card)
- Network interfaces (WiFi/Ethernet/cellular)
- OTEL collector (present or not)
- Supported runtimes (e.g., OCI)
- Supported deployment types (e.g., Helm)

The Target Name describes the Compute Target itself and carries no security meaning; the identity a client authenticates with is issued through the [Margo Identity and Authorization Framework](../identity/identity-and-trust.md).

## Relevant Links

Please follow the subsequent links to view more technical information on capability reporting:

- [Device Capabilities API](../../specification/margo-management-interface/device-capabilities.md)
