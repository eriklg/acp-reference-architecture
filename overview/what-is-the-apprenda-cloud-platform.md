# What is the Apprenda Cloud Platform?

Apprenda is system for .NET, Java, and containerized applications where application workloads are first-class citizens of the architecture. Apprenda aggregates host Windows and Linux infrastructure into an abstracted single pool of compute resources that becomes a multitenant self-service platform for development teams.  Developers interact with the platform through a collection of interfaces and APIs, instructing it to deploy, scale, configure, and otherwise manage their application workloads.

An application running on Apprenda is one that is composed of some combination of the following:
* .NET
  * IIS-hosted ASP.NET UI (MVC, WebForms, etc.)
  * Self-hosted .NET WCF Web Services
  * Stand-alone Windows Services
* Java
  * Java Web Applications (WAR or JAR deployment model)
  * Java Web Applications (J2EE)
* Containers
  * Docker images
* Databases
  * SQL Server Database
  * Oracle Database

Apprenda’s core architectural components described in this document work together to orchestrate deployment, scaling, fault tolerance, access, and more for guest applications.  Additionally, Apprenda exposes consumable shared services out of the box such as an ESB, distributed caching, application metering and monitoring, and more.  Through a plugin model, called Add-Ons, the platform can be expanded to offer any system as a shared service to guest applications.

Through APIs and additional backend features, Apprenda gives owners many options for operationalizing the platform.  Incorporating existing enterprise systems for change control, policy enforcement, and more is possible using the operator’s interfaces.

The best way to think of Apprenda is from a stack-wise point of view. Apprenda is analogous to an operating system, an application server like IIS or Tomcat, or any other pure software layer that sits above physical resources (such as hardware or a network) and acts as a host and execution backdrop for an application that lives on top of it. In the case of an operating system, everything from memory subsystems to disk access and thread scheduling is provided as a set of services to the applications built for the OS. When you write code, you implicitly assume that the OS will take care of fundamental and difficult problems for you, and that the hardware resources are abstracted away from your code to some extent. Runtimes like the .NET CLR or the JVM provide further value through more abstraction for a large subset of applications being developed. Apprenda is similar in both form and spirit to an operating system or runtime.  

_Here are some of the Apprenda Cloud Platform’s notable features and use cases_:

* A multi-machine application server and runtime for hosting and managing applications.
* REST and SOAP exposure of API endpoints for web service integration and automation.
* Instrumentation and transformation engines that virtualize your application’s components across tenants so that you can achieve high efficiency. This means that parts of your application, such as your database, can be written as if they were for one tenant or customer (e.g., storing row data naively with no notion of tenant ownership), but, when running on Apprenda, can be transformed to behave in a multi-tenant fashion (e.g., your database will be instrumented to support multiple tenant data storage in a way that is transparent to your application queries). This instrumentation is optional, and a development team may choose to use it in scenarios where their application architecture calls for it.
* A user and tenant management layer that your applications can leverage so that the idea of users and account information can be shared across applications.
* An API and set of associated services that provide fundamental building blocks for user/account management and provisioning (either by you or through pre-built storefront widgets that allow your customers to self-provision), caching, and message brokering (among other things).
* Containerized application deployment via Docker.
* Enterprise class server mechanics such as automatic high availability of web services, linear scale-out across your server farm, automatic and seamless IIS-based web farming, and failure isolation for both Windows and Linux servers.
* A Resource Allocation Policy (RAP) management system that allows IT to “slice” the sum of the compute power under control by the Apprenda Platform into discrete units of allowed CPU and memory allocation.  Development teams can then choose these “slices” and assign them to their application components.  The Platform will monitor and throttle resource utilization based on assigned policies.  This gives IT advanced capacity planning capabilities and development teams concrete expectations while shielding them from the underlying infrastructure in the spirit of a PaaS.
* A set of web portals and tools to manage your applications and customers.
* An administrative web portal that gives IT a detailed view of how the Platform “sees” the infrastructure and how it has distributed application components accordingly.
APIs for integration with enterprise monitoring, logging, and other tools for use in an SRE practice.
