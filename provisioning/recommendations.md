
# Hardware and Software Recommendation Specs

The following specs are recommendations based on platform role, underlying operating system requirements, communication needs, and more.  These are not hard guidelines.  The intention of these recommendations is to give you an understanding of the base compute requirements and the beginning of how these components interact with each other.

If your deployment is in a public cloud such as AWS, Azure, Google Cloud, or Bluemix, consult with Apprenda's services team to make the appropriate machine sizing and infrastructure selections.  We have reference architectures specific to these public cloud providers.


| Platform Role  | Description    | Hardware       | Software       |
| :------------- | :------------- | :------------- | :------------- |
| Load Manager, Quantity: 2 machines | Runs IIS for the purpose of acting as a reverse proxy to servers that host guest application UI workloads. | <ul><li>Dual Core CPU</li><li>4GB RAM</li></ul> | <ul><li>Windows Server 2012/2012 R2 Datacenter or Enterprise</li><li>.NET Framework 4.5+</li><li>IIS 8/8.5 (Web Server Role)</li><li>Latest version of MS Application Request Routing Module</li></ul> |
| Coordination Node<sup>1</sup>, Quantity: 3 machines | Runs the Apprenda Control agent that orchestrates routing and deployment of guest application workloads. Requires an odd number of instances. | <ul><li>Dual Core CPU</li><li>8GB RAM</li></ul> | <ul><li>Windows Server 2012/2012 R2 Datacenter or Enterprise</li><li>.NET Framework 4.5+</li></ul> |
| Cache Node<sup>1</sup>, Quantity: 3 machines | Runs the Apprenda Caching service that provides in-memory caching for Windows and Linux servers. | <ul><li>Dual Core CPU</li><li>8GB RAM</li></ul> | <ul><li>Windows Server 2012/2012 R2 Datacenter or Enterprise</li><li>.NET Framework 4.5+</li></ul> |
| Windows Worker Node, Quantity: _n_ | Runs Windows-based application workloads.  With IIS also hosts .NET frontend applications. | <ul><li>Multi Core CPU</li><li>16GB RAM</li></ul> | <ul><li>Windows Server 2012/2012 R2 Datacenter or Enterprise</li><li>.NET Framework 4.5</li><li>IIS 8/8.5 (Web Server Role)</li><li>iisnode</li> |
| MS SQL Node<sup>2</sup>, Quantity: 2 (x2 for failover clustering) | Provides persistence for core Apprenda components and DBaaS capabilities for guest applications.  Recommendation is to use one instance for core Apprenda database, and a separate instance for guest app DBaaS. | See: [https://docs.microsoft.com/en-us/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server](https://docs.microsoft.com/en-us/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server) | See: [https://docs.microsoft.com/en-us/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server](https://docs.microsoft.com/en-us/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server) |
| Repository, Quantity: 1 | Network share that will serve as the repository for all Platform and guest application binaries. | <ul><li>SAN or NAS<sup>3</sup></li></ul>| |
| _Optional_: Oracle 12C | Provides DBaaS capabilities for guest applications with Oracle RDBMS requirements. | See: [http://docs.oracle.com/database/121/](http://docs.oracle.com/database/121/) | See:  [http://docs.oracle.com/database/121/](http://docs.oracle.com/database/121/) |
| _Optional_: Linux Worker Node, Quanity: _n_ | Runs Apprenda’s Linux container to host Java application workloads.  _With Docker installed provides container deployment capabilities._ | <ul><li>Multi Core CPU</li><li>16GB RAM</li></ul> | <ul><li>RHEL 7</li><li>CentOS7</li><li>Alternative Linux distros (verify w/ Apprenda)</li></ul> |
| _Optional_: ADFS Node, Quantity: 2 | Provides enterprise federated identity (SSO) capabilities using Active Directory Federation Services. | See: [https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/design/ad-fs-requirements](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/design/ad-fs-requirements)| See: [https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/design/ad-fs-requirements](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/design/ad-fs-requirements) |

<sup>1</sup> Coordination and Cache node roles may share machines

<sup>2</sup> Refer to your organization's SQL requirements for initial setup.  Apprenda's configuration requirements are documented in the Pre-Install Checklist (PICL).

<sup>3</sup> The repository may be hosted on any of the machines so long as the network path is accessible from all other machines.
