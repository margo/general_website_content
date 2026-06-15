# Device Capabilities

The purpose of device capabilities reporting is to ensure the Workload Fleet Management (WFM) solution has the information needed to pair workloads with compatible edge devices. The device's capabilities are reported to the WFM web service using the [Device Capabilities API](../../specification/margo-management-interface/device-capabilities.md).

**Note:** _Devices report only the capabilities that are explicitly exposed and accessible to Margo workloads. If a device feature is isolated from the Margo runtime environment, it is excluded from the capabilities report. For example, an onboard camera used exclusively for local device security—and completely isolated from Margo—is not reported as an available capability. This ensures workloads are not scheduled against unavailable or restricted hardware resources._

### Device Capability Reporting

The device owner reports their device's capabilities and characteristics, via the device API, when onboarding the device with the Workload Fleet Management solution. Additionally, during the lifecycle of the edge device, if there is a change that impacts the reported characteristics, the device updates the Workload Fleet Manager with the latest information via the [Device Capabilities API](../../specification/margo-management-interface/device-capabilities.md). 

The following information is exchanged:

- Device Id
- Device Vendor
- Model Number
- Serial Number
- Margo Device Role Designation(Cluster Leader/Worker / Standalone Device)
- Resources available for workloads to utilize on the Device:
    - Memory Capacity
    - Storage Capacity
    - CPU information
- Device peripherals(i.e. Graphics card)
- Network interfaces(wifi/eth/cellular)

## Relevant Links

Please follow the subsequent links to view more technical information on device capability reporting:

- [Device Capabilities API](../../specification/margo-management-interface/device-capabilities.md)