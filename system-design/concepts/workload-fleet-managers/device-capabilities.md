# Device Capabilities

The purpose of device capabilities reporting is to ensure the Workload Fleet Management (WFM) solution has the information needed to pair workloads with compatible edge devices. The device's capabilities are reported to the WFM web service using the [Device Capabilities API](../../specification/margo-management-interface/device-capabilities.md).

**Note:** _Devices report only the capabilities that are explicitly exposed and accessible to Margo workloads. If a device feature is isolated from the Margo runtime environment, it is excluded from the capabilities report. For example, an onboard camera used exclusively for local device security—and completely isolated from Margo—is not reported as an available capability. This ensures workloads are not scheduled against unavailable or restricted hardware resources._

### Device Capability Reporting

The device reports its capabilities and characteristics, via the device API, when the device's client first connects to the Workload Fleet Management solution. Additionally, during the lifecycle of the edge device, if there is a change that impacts the reported characteristics, the device updates the Workload Fleet Manager with the latest information via the [Device Capabilities API](../../specification/margo-management-interface/device-capabilities.md).

A workload hosting device exchanges the following information:

- Device Id
- Device Vendor
- Model Number
- Serial Number
- Resources available for workloads to utilize on the Device:
    - CPU information
    - Memory Capacity
    - Storage Capacity
- Device peripherals (e.g., graphics card)
- Network interfaces (WiFi/Ethernet/cellular)
- OTEL collector (present or not)
- Supported runtimes (e.g., OCI)
- Supported deployment types (e.g., Helm)

## Relevant Links

Please follow the subsequent links to view more technical information on device capability reporting:

- [Device Capabilities API](../../specification/margo-management-interface/device-capabilities.md)
