# Hardware
The hardware needed for the deployment of the Apprenda Platform in this reference architecture covers various Platform roles: web servers, application servers, database servers, and ancillary servers.  Our reference architecture is intended to cover deployment scenarios for high availability.  We’ve configured away all single points of failure.  In most cases, the Platform’s architecture accounts for high availability; however, in the few cases where the product’s design itself does not supply HA, we rely on standard practices in Windows environments such as SQL Server clustering.

## Machines

### Bare Metal vs. Virtual Machines
The Apprenda Platform sits atop the Microsoft Windows and Linux operating systems, and as such, relies on the OS to abstract away specific hardware interaction and concerns. Apprenda can run on bare metal, virtual machines, IaaS, or a hybrid approach so long as OS and networking requirements are satisfied. This reference architecture includes a recommendation for spreading VMs across hosts for failure containment should your approach be virtualized.

## Networking

There are two primary networking concerns when working with the Apprenda Platform:
* Networking the participating machines together in a primary LAN configuration so that they have hostname resolution and uninterrupted access to each other via TCP.
* Providing HTTP and HTTPS access (and necessary DNS) to for the purpose of accessing guest application components running atop and within your platform.  This is known as ingress.

### Establishing a Private LAN for Apprenda Nodes
The servers being deployed to support a unique instance of the Apprenda Platform should be setup in a DHCP network configuration whereby they obtain IP addresses from a gateway server or networking appliance.  For Platform operations, the servers communicate with each other using DNS-resolvable hostnames, and therefore require an internal DNS structure to be in place that resolves IP assignments.  This can be an existing DNS infrastructure or one dedicated to the Apprenda Platform servers.  Our reference architecture specifies a dedicated Domain Controller that also acts as the primary DNS server for all servers on one Platform instance’s private network.

### Inbound Traffic (Ingress)
The first point of contact for any inbound request to a Platform hosted application component URL is one of the Load Manager servers.  This is true for UI workloads running on frontend servers, service workloads running on application servers, and Java Web application workloads running on Linux servers.    We also recommend placing a hardware load balancer of your choice in a DMZ in front of the entire environment, routing traffic via ports 80 and 443 (HTTP and HTTPS respectively) between the Load Manager servers in either an active/active (HA) configuration or an active /passive (failover) configuration. As in standard web hosting environments, the Platform, its portals, and guest application UIs will all be accessible at a URL specified by you during Platform installation.  You will need to configure external DNS that routes requests for your Platform URL to the hardware load balancer or the Load Manager server(s) directly.  Traffic to Load Manager servers from all Apprenda-provided utilities and products occurs over ports 80 and 443.  The Apprenda Load Manager distributes requests to the proper frontend content servers based on guest app workload location, and uses port 8080 by default internally (this is considered “inside” Apprenda proper).  A typical HTTP request on port 80 will reach the Load Manager and be routed internally on port 8080 to a frontend content server that has the appropriately requested guest application installed and configured (this may be multiple web servers due to web farming).  The response is sent back out through the proxy on port 80 so translation and internal routing is transparent to the requester.

## Using a SAN Device for Storage
The use of a SAN or NAS is recommended as the physical storage mechanism for the following primarily because it offloads the concerns of data backup and recovery.  Typically, there are two use cases for setting up network attached storage:
* The Platform Repository: a network share that will serve as the central storage location for all Platform and guest application binaries. This location must be configured prior to installation, should be specified as a network path in the Apprenda Installer, and must contain the following three folders:
  * Applications
  * Apprenda
  * SAC
* A central location for SQL failover cluster storage; this will be required to set up the recommended SQL failover clusters prior to running the Apprenda Installer
