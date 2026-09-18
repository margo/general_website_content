# Gateway Services

A Margo gateway service allows one or several non-Margo devices to connect to and be managed by a Margo Workload Fleet Manager (WFM). The service translates communication between those devices and the WFM, so hardware that cannot host a Margo client of its own is still presented to the WFM as a Compute Target.

A Margo gateway service could run on a server, within a device, or on a dedicated device. The service is the Margo concept in each case; hardware dedicated to running it is commonly called a gateway device, but that describes where the service runs rather than a distinct kind of Margo component.

Gateway services determine how downstream devices appear to the WFM as Compute Targets, and can be divided into 3 types:

* **Transparent gateway services** are not visible by the WFM. They provide a Margo client for each downstream device they connect, so each device appears to the WFM as its own Compute Target.
* **See-thru gateway services** are visible to the WFM, they act on behalf of one or more downstream devices and each device is visible to the WFM. They host a single Margo client for all the downstream devices they connect and present each device as a separate Compute Target with its own capabilities.
* **Opaque gateway services** hide the downstream devices they connect to the WFM, presenting a single Compute Target with the combined capabilities of all the downstream devices they connect.

In every case the WFM deploys workloads to a Compute Target, not to hardware directly, so a Compute Target does not necessarily map one to one onto a physical device.

![Gateway Types](../../figures/gateway-types.drawio.svg)
