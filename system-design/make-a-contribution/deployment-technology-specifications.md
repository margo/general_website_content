# Deployment Technology Spec Writing Requirements

> **Note**: This document is being worked on as part of ongoing efforts to split out the core specification from the individual deployment technology specifications. If will be updated as those efforts progress.

## Overview

In order to decouple support for different deployment technologies (e.g, Helm, Compose, Wasm, Quadlets, etc.) from Margo's core specification we have adopted the use of independent deployment technology specifications. These independent deployment technology specification allows the choice of technologies to evolve over time without impacting Margo's core specification.

This document provides the requirements and guidelines for people to follow when creating and contributing to deployment technology specifications. These are requirements for the specification authors to follow, not specification implementors.

## Profile Characteristics

Each deployment technology specification is responsible for defining the applicable [profile](../specification/margo-management-interface/profiles) characteristics usable with the specification.

### Characteristic definitions and evolution

Each characteristic MUST publish a human-readable definition and MAY publish a JSON Schema. The characteristic definition MUST be published, or referenced, as part of the applicable deployment technology specification. The schema is informative to a workload fleet manager operating in passthrough mode, but is normative for device suppliers claiming conformance to the characteristic if a schema is provided.

Characteristics keys must be globally unique and should following the recommended naming guidelines:

- The key name SHOULD follow the pattern `{domain}/{category}/{identifier}` or `{domain}/{identifier}`
- The domain for all Margo community characteristics most be `margo.org`
- The domain for vendor-specific characteristics defined in vendor-specific deployment technology specifications SHOULD use an appropriate domain for the company or organization creating the specification.
- The key for a deployment technology characteristics MUST use `{domain}/deployment/{technology-identifier}`

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

Each deployment characteristic (e.g., `margo.org/deployment/helm`) describes what is required for an application to be matched with suitable workload targets using the required properties. Each deployment characteristic can define what properties make sense for that specific deployment technology. Deployment characteristics not expected to be common between deployment technology specifications.

## Vendor-Specific Deployment Technology Specifications

Vendors requiring support for deployment technologies not defined by the Margo community can create their own deployment technology specification to facilitate collaboration between application and device suppliers. Since the Margo community does not maintain a listing of these vendor-specific deployment specifications, it is expected suppliers collaborate in order to know what is available.

The use of custom deployment technologies adds functionality not part of the Margo specification. Vendors implementing their own deployment technology specification SHOULD following the requirements in this document.
