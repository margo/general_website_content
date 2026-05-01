# Margo Initiative - Version Management Strategy
## Purpose

The purpose of this document is to establish a version management strategy for the Margo initiative. This version management outline covers the major deliverables the Margo initiative will be responsible for.

The goal is to make public releases easy to understand, keep preview builds useful for feedback, and ensure all official deliverables can be versioned together at release.

## Recommended Direction

Margo intends to use one public semantic version for the official Margo release(s) and apply it to these deliverables at release time:

Current Preview Release deliverables include:
- Specification
- Open API Specification(s)
- Code first sandbox

The following will be delivered at the time of our first General Release 1:
- Reference Implementation
    - includes various software components
- Conformance Test Toolkit(CTT)
    - includes various software components

The specification remains the release anchor. The other three deliverables inherit the same public version when they are published as part of the same official release.

This keeps the release story simple:

- Preview work can happen frequently without creating misleading public version jumps
- Public releases only increment one semantic version field at a time
- All official deliverables for a given release are clearly compatible with each other

## Versioning Model

### General Availability(GA) release versions

Official releases should use plain semantic versioning with no GA suffix:

- `1.0.0`
- `1.0.1`
- `1.1.0`
- `2.0.0`

The release number should advance based on the highest level of accepted change since the previous public release:

| Change in release scope | Next public version | Rule |
| --- | --- | --- |
| Clarifications, corrections, non-breaking fixes only | PATCH | `1.0.0 -> 1.0.1` |
| One or more non-breaking additions or new features | MINOR | `1.0.0 -> 1.1.0` |
| One or more breaking changes | MAJOR | `1.0.0 -> 2.0.0` |

When multiple change types exist, the release should use the highest-precedence change type:

- Major supersedes minor
- Minor supersedes patch
- Patch does not increment if a minor or major release is already required

SemVer itself defines what major, minor, and patch mean, but this precedence rule is a release management policy built on top of those semantics.

### Preview Release(PR) deliverables before release

Preview release deliverables should use preview release labels instead of incrementing the public semantic version for every change implemented.

These PR deliverables are not official releases of the specification. They are feedback checkpoints that show the suppliers/community what is being prepared for the next official release.

Margo plans to publish preview release checkpoints quarterly on the 15th day of each quarter-end month:

- March 15
- June 15
- September 15
- December 15

The version semantics documented in this plan still apply to each preview checkpoint. The scheduled quarterly drop determines when a preview is published, not how the semantic version is classified.

Recommended labels:

- `alpha.N` for pre-draft working versions
- `beta.N` for draft versions under broader review
- `rc.N` for coordinated release candidates when all release deliverables are assembled and being validated

Examples:

- `1.0.0-alpha.1`
- `1.0.0-alpha.12`
- `1.0.0-beta.3`
- `1.1.0-rc.1`

The base semantic version in the preview tag should represent the next intended public release. That means:

- Before the first official release, preview versions target `1.0.0`
- After `1.0.0` is released, if the next release is expected to be a non-breaking feature release, previews move to `1.1.0-alpha.1`
- If later work introduces a breaking change, previews move to `2.0.0-alpha.1`

This preserves semantic meaning while still allowing frequent preview publication without treating each internal change as a released specification version.

## Deliverable Plan

### Specification & Documentation

The Specification and supporting documentation is the authoritative driver for release classification.

- `alpha.N` represents `pre-draft` working snapshots for feedback
- `beta.N` represents `draft-stage` review snapshots for feedback
- Optional `rc.N` represents final coordinated validation snapshots
- Final publication removes the suffix and publishes the plain semantic version

Release decisions for patch, minor, or major should be based on specification impact:

- `Patch` for clarifications, corrections, and non-breaking wording updates
- `Minor` for new non-breaking capabilities or normative additions
- `Major` for normative breaking changes

### OpenAPI specification

The OpenAPI specification should share the same public release version as the specification because it describes the same release contract.

- Preview versions should mirror the specification version exactly
- Final GA release should publish the same semantic version as the specification
- If the OpenAPI document changes in a way that changes the contract, that change must be considered in the release classification

Examples:

- Spec `1.1.0-beta.2` -> OpenAPI `1.1.0-beta.2`
- Spec `1.1.0` -> OpenAPI `1.1.0`

### Reference Implementation

The reference implementation should be versioned to the same release as the specification at official release.

- Public release version matches the specification version it implements
- Preview builds use the same target semantic version with `alpha`, `beta`, or `rc` labels
- Implementation-only iteration between previews should increase the pre-release sequence rather than minting a separate public version line

Examples:

- Specification target `1.1.0-alpha.4` -> Reference implementation `1.1.0-alpha.4`
- Official release aligned to `1.1.0` -> Reference implementation `1.1.0`

If the reference implementation uncovers a breaking issue in the specification, the release classification should be revised before the next preview or release is published.

### Conformance test and toolkit

The conformance suite should validate one specification release at a time and should carry the same public version as the release it verifies.

- Public release version matches the specification and OpenAPI specification
- Preview versions follow the same pre-release label sequence
- Toolkit updates that change expected behavior must feed back into release classification before GA

Examples:

- Conformance test for spec `1.0.0-beta.3` -> toolkit `1.0.0-beta.3`
- Conformance package published for GA `1.0.1` -> toolkit `1.0.1`

## Release Cohesion Rule

At an official release, all four Margo deliverables should publish the same public version number:

| Deliverable | Release version at GA 2 example |
| --- | --- |
| Specification | `1.1.0` |
| OpenAPI specification | `1.1.0` |
| Reference implementation | `1.1.0` |
| Conformance test and toolkit | `1.1.0` |

This does not mean every artifact must be regenerated for trivial editorial work, but it does mean every official release package should declare the same release version so users can understand compatibility immediately.

## Sandbox Relationship

The sandbox should keep its own release cycle, as described in [Sandbox Release Document](https://github.com/margo/sandbox/blob/main/docs/release.md). It is a supporting implementation environment to enable the code first process, not the authoritative version anchor for the specification.

Recommended relationship:

- Sandbox implementation depends on the open API spec within the specification. Changes to specification should be reflected in the sandbox at the next convenient release. 
- Sandbox retains its own SemVer and release automation
- Sandbox release notes should state which specification release they align to
- Sandbox tags may use release candidates and nightly builds independently of the specification deliverables
- Sandbox changes do not force a specification version bump unless they reflect an accepted specification change

Example compatibility statement:

- Sandbox `v0.8.0` aligns with Margo release `1.1.0`

This preserves the useful sandbox process from the existing release document without coupling sandbox cadence to specification governance.

## Estimated Workflow

### Phase 1: Pre-draft work

- Publish working previews as `X.Y.Z-alpha.N`
- Target quarterly preview publication on March 15, June 15, September 15, and December 15
- Increment `N` for each preview drop or agreed checkpoint
- Use issue and branch tags to track PR numbers or work items instead of embedding PR identifiers in the semantic version

### Phase 2: Draft review

- Promote previews to `X.Y.Z-beta.N` once the working group is ready for broader review
- Continue using the quarterly preview publication target unless an exception is approved
- Continue incrementing `N` as draft issues are resolved
- Restrict changes to issues that still affect release readiness

### Phase 3: Coordinated release validation

- Assemble the specification, OpenAPI specification, reference implementation, and conformance toolkit on the same target version
- Optionally publish `X.Y.Z-rc.N` when the team wants a formal release-candidate gate
- Validate that all four deliverables still align to the same contract

### Phase 4: Official release

- Publish the plain semantic version with no suffix
- Release all four official deliverables on that same version number
- Publish release notes that explain whether the release is patch, minor, or major and why

## Initial Baseline Proposal

Based on the current notes, the cleanest starting point is:

- First official public release: `1.0.0`
- Pre-release work before that publication: `1.0.0-alpha.N` and `1.0.0-beta.N`
- After `1.0.0`, determine the next target release by the highest accepted change class

Illustrative progression:

1. Working group preview: `1.0.0-alpha.1`
2. Later pre-draft snapshot: `1.0.0-alpha.7`
3. Draft review package: `1.0.0-beta.1`
4. Coordinated release candidate: `1.0.0-rc.1`
5. First public release: `1.0.0`
6. Next feature-bearing preview after release: `1.1.0-alpha.1`
7. Next feature-bearing public release: `1.1.0`

## Governance Rules To Adopt

- The specification change classification determines the next public release number
- Public releases never include `GA1`, `GA2`, or PR counters in the version string
- Preview identifiers belong in pre-release labels only
- PR numbers, work item identifiers, and branch details should be tracked through repository tags, release notes, and changelogs rather than encoded into the version number
- All official release deliverables publish the same release version
- Sandbox publishes its own version and declares compatibility to the release

## Open Decisions For Follow-Up

These items should be settled before the first formal rollout of the process:

- Decide whether `rc.N` is required or optional for every official release
- Define who approves the move from `alpha` to `beta` and from `beta` to release
- Define the minimum entry criteria for publishing the reference implementation and conformance toolkit in the same release
- Define where the compatibility matrix between sandbox releases and specification releases will live
- Decide whether build metadata is needed for internal-only artifact rebuilds that do not change release semantics


## Tasklist to implement

- Receive feedback and review the proposal above
    - Once all feedback is folded in, implement within infrastructure. 
- Create a branching strategy in the following repositories:
    - Specification
    - General website content
    - conformance documentation
- Implement version management strategy at our PR2 release










---------------Older Content Below----------------------------
# GOAL:
Create a concrete version management strategy across the various deliverables Margo maintains. This will be critical as we iterate moving towards our first GA release. 

## Proposed Strategy:
Utilize symantec versioning outlined in the following Markdown:
- https://docs.margo.org/margo-specification-versioning#specification-maturity-stages
- Determining factor is the scale of changes changes and whether breaking / med / small changes/fixes

## Specification
> Note following steerco meeting on version management of the specification. 
- Team decided we wanted to move towards the following version management of the specification
- `pre-draft`-`generalrelease`-`release`
    - Applying this rule to our next release, we will need a tagged main branch that triggers the website update, to utilize the following version
        - `pre-draft-GA1-PR2`
        - Next quarterly release will be `pre-draft-GA1-PR3`
 
- Current state: no version right now: “Pre-Draft” stage
- Decoupled from sandbox deliverable/versions other than:
    - Workload Management API linkage between sandbox
        - API is version `1.0.0`(currently)
        - **[PROPOSAL]** revert the version back to `0.1.0-pre-draft-GA1-PR1`
            - 0.1.xxx-pre-draft-
        - What are the rules for version numbers per major release
            - Software
                - reference imp
                - conformance test
           -  and specification carrying same number!
               - Specification: 1.0.200
               - Open API spec and other deliverables: 1.0.200
               - 
  - Initial release GA1
      - 1.0.0 - spec version and open API specification
      - then we have preview releases which could result in 1.20.500....
  - Release GA2
      - Do we carry over 1.20.500 or increment from 1.0.0??
      - 
------
## Sandbox
Additional collateral around proposed version management within the Sandbox repository. 
    - SEE [HERE]https://github.com/margo/sandbox/blob/main/docs/release.md) 
- Whole sandbox deliverable to get a version upon the next release. 
    - versioning not so important as specification or other official deliverables
    - Change log of this deliverable is crucial to inform users of updates, and whether it's worth their time to tear down and redeploy the whole sandbox, just pieces, or ignore the release. 

-----
## FUTURE (GA Release will cement versioning of these items)
### Conformance test
- To be versioned with specification
### Reference implementation
- To be versioned with specification
------

# Additional Tasks:
- Need to create a notification channel for releases Sandbox
