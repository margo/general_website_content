# Deployment Technology Spec Writing Requirements

> **Note**: This document is being worked on as part of ongoing efforts to split out the core specification from the individual deployment technology specifications. It will be updated as those efforts progress.

## Overview

In order to decouple support for different deployment technologies (e.g., Helm, Compose, etc.) from Margo's core specification, we have adopted the use of independent deployment technology specifications. These independent deployment technology specifications allow the choice of technologies to evolve without impacting Margo's core specification.

This document provides the requirements and guidelines for people to follow when creating and contributing to deployment technology specifications. These are requirements for the specification authors to follow, not specification implementors.

## Specification Constraints

- Deployment technology specifications MUST define the deployment technology key associated with the specification. See the [Profile Characteristics](#profile-characteristics) section below.
- Deployment technology specifications MUST follow Margo's [Version Management Strategy](../specification/specification-version-management) for versioning, repository branching, and releases. Deployment technology specifications are versioned independently from Margo's core specification.
- Deployment technology specification MUST package deployed workload artifacts, referenced by the Application Description's `deploymentProfiles[].component[].properties.repository`, as OCI blobs and MUST define how those artifact OCI blobs are created.
- Deployment technology specification MUST define how workload targets are expected to deploy the workloads and highlight any special constraints needing to be followed by either the application or workload target suppliers.
- Deployment technology specification MUST rely only on the APIs defined in the Margo core specification and MUST NOT introduce any new APIs or attempt to modify existing APIs.
- Deployment technology specifications MUST rely only on workload fleet manager suppliers implementing logic defined in the Margo core specification only and MUST NOT require workload fleet manager suppliers to implement logic specific to the deployment technology specification.
- Deployment technology specifications MUST NOT rely on workload fleet manager suppliers understanding characteristic schemas defined as part of the specification.
- Deployment technology specifications MAY define their own profile characteristics or reference common characteristics defined by the Margo community.

> **Note:** We are interested in hearing about any use cases where there is a desire to include additional characteristic properties that are intended for workload fleet managers to use if a workload fleet manager chooses to tightly couple their implementation to a deployment technology specification.

## Governance

> **Note:** The details for how deployment technology specification governance is handled will be provided once the process is finalized.

## Profile Characteristics

Each deployment technology specification is responsible for defining the applicable [profile](../specification/margo-management-interface/profiles) characteristics usable with the specification.

### Characteristic definitions and evolution

Each characteristic MUST publish a human-readable definition and MAY publish a JSON Schema. The characteristic definition MUST be published, or referenced, as part of the applicable deployment technology specification. The schema is informative to a workload fleet manager, but is normative for device suppliers claiming conformance to the characteristic if a schema is provided.

Characteristic keys MUST be globally unique and follow the naming guidelines:

- The key name SHOULD follow the pattern `{domain}/{category}/{identifier}` or `{domain}/{identifier}`.
- The domain for all Margo community characteristics MUST be `margo.org`.
- The domain for vendor-specific characteristics defined in vendor-specific deployment technology specifications SHOULD use an appropriate domain for the company or organization creating the specification.
- The key for a deployment technology characteristic MUST use `{domain}/deployment/{technology-identifier}`.

Characteristics are not versioned by adding a version field to each instance. A characteristic owner MAY make the following additive changes only under the same key:

- add new properties; or
- add an enum option; or
- make an optional property required

These additive changes allow existing application description [match expressions](../specification/applications/application-description#characteristics-attributes) to continue working because what was being matched has not changed.

The characteristic owner MUST assign a new key for any destructive type change. The following are considered destructive changes:

- removing or renaming a property; or
- changing a property data type; or
- removing an enum option; or
- making a required property optional.

These types of changes could potentially break existing application definition match expressions, which is why a new key is created so the existing application definitions are not affected.

In order to reduce compatibility concerns, modifying a characteristic in such a way as to require a new unique key is NOT RECOMMENDED and should only be done when there are no other options available.

Characteristics SHOULD strive to keep the required properties to an absolute minimum to prevent application suppliers from having to define a lot of matching expressions that are unnecessary for all conditions.

The workload fleet manager MUST NOT be required to do any conversions between what is in the Application Description and Profile. For example, where units are important to the property, each characteristic MUST define a single unit the value is expected to be in, so no unit conversion logic is required.

#### Deployment characteristics

Each deployment characteristic (e.g., `margo.org/deployment/helm`) describes what is required for an application to be matched with suitable workload targets using the required properties. Each deployment characteristic can define what properties make sense for that specific deployment technology. Deployment characteristics are not expected to be common between deployment technology specifications.

## Vendor-Specific Deployment Technology Specifications

Vendors requiring support for deployment technologies not defined by the Margo community can create their own deployment technology specification to facilitate collaboration between application and device suppliers. The use of custom deployment technologies adds functionality not part of the Margo specification. Since the Margo community does not maintain a listing of these vendor-specific deployment specifications, it is expected that suppliers collaborate in order to know what is available.

Vendors implementing their own deployment technology specification SHOULD follow the requirements in this document.
