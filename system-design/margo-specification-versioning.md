## **Margo Specification Versioning Strategy**

### **Understanding Version Numbers**

Margo follows semantic versioning principles to communicate the maturity and stability of each specification release clearly:

- **Major version (first number - v1.0)**: Increments when specifications reach general availability or include significant, potentially breaking changes
- **Minor version (second number - v1.1)**: Increments for incremental improvements, clarifications, or non-breaking additions within a major release
- **Patch (third number - v1.1.1)**: increase the version when you apply bug fixes that are backwards compatible.

<img width="660" height="413" alt="image" src="https://github.com/user-attachments/assets/0fce57cc-cc29-4553-9f1e-f195e0971498" />

### **Specification Maturity Stages**

**1. Pre-Release (PR)**
- Purpose: Early community engagement and real-world validation - indicates a version that is unstable and not ready for production
- Stability: Low—breaking changes likely
- Use case: Experimental implementations, plugfest testing, proof-of-concept development
- Feedback: Actively encouraged through GitHub issues and working group discussions

**2. Draft**
- Purpose: Refinement and formal review by the Steering Committee
- Stability: Moderate—minor adjustments possible
- Use case: Pilot implementations, vendor evaluation
- Feedback: Accepted for significant technical issues only
> During this phase, the Working Group (WG) formally reviews the documents it has developed. Once the review phase is complete, the documents must be approved by the WG before being submitted to the Steering Committee (SC) for formal ratification.


**3. General Release (GA)**
- Purpose: Production deployment
- Stability: High—changes follow formal RFC processes
- Use case: Production systems, vendor commitments, certification programs
- Feedback: Must follow the established change request procedure

> After the Working Group (WG) reviews and approves the documents, they are forwarded to the Steering Committee (SC) for formal ratification. Once ratified by the SC, the documents become ready for publication.
