# Workload Target Profiles

The purpose of workload target profile reporting is to ensure the Workload Fleet Management (WFM) solution has the information required to [match workloads](../../specification/applications/application-description#characteristics-attributes) with compatible workload targets. WFM implementation are not required to understand each characteristic's schemas and instead only use the information for matching. This allows the independent deployment technology specifications to be added or evolve without requiring updates to the WFM implementation.

The workload target's profile is reported to the WFM web service using the [Profile API](../../specification/margo-management-interface/profiles.md).

**Note:** _Workload targets report only the characteristics explicitly exposed and accessible to Margo workloads. If a characteristic is isolated from the Margo runtime environment, it is excluded from the profile report. For example, an onboard camera used exclusively for local device security—and completely isolated from Margo—is not reported as an available characteristic. This ensures workloads are not scheduled against unavailable or restricted hardware resources._

## Profile Reporting

The workload targets report their profile characteristics, via the Profile API, when the workload target's client first connects to the Workload Fleet Management solution. Additionally, during the lifecycle of the workload target, if there is a change that impacts the reported characteristics, the workload target updates the Workload Fleet Manager with the latest information via the [Profile API](../../specification/margo-management-interface/profiles.md).

The profile characteristics reported are determined by the different deployment technologies the workload target supports as defined in each applicable deployment technology specification.

> **Note:** While we are working on splitting out the core specification from the independent deployment technology specifications, common profile characteristics are [indicated here](../..//specification/margo-management-interface/profiles#common-characteristics).

## Relevant Links

Please follow the subsequent links to view more technical information on profile reporting:

- [Profile API](../../specification/margo-management-interface/profiles.md)
