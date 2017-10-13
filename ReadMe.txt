Micro Services
01) Leveraging micro services allows you to deployment and version services independently without affecting other parts of the system.
02) Each service should have it's own database and data model. They can be written in any language and use any type of DB (SQL or NOSQL)
03) A microservice should handle one type of business capability
	Code solves a domain specific problem
	Built by small team using a particular technology stack
	Exposes features to caller via a well-defined API contract
	Degrades gracefully when dependent services fail
	Can be upgraded independently of calling services (rolling upgrade)
	Dividing a big service into smaller services is often referred to as a microservices architecture
04) Scalable service considerations
	You need to dynamically scale services to manage tension between processing requests quickly and cost
	Clients dynamically discover services to communicate (via a load balancer or a service registry)
	Data must be partitioned for size/speed, shard
	Diagnostic info for all instances are buffered locally and periodically archived in a central, external store
05) Pain Points
	More services means more netwokr communication
		Decreases overall performance due to network hops and (de)serialization
		Requir3es more failure (timeout) recovery code
	Hard to test in isolation without dependent services
	Hard to debug/monitor across services
	New service versions must support old & new API contracts simultaneously because client services don't upgrade at the same time
	Devs are trading short-term pain for long-term gain
06) 12-Factor Apps
	Single root repo; don't share code with another app
	Deploy dependent libs with app
	No config in code; read from environment vars
	Handle unresponsive app dependencies robustly
	Strictly separate build, release, & run steps
		Build: Builds a version of the code repo & gathers dependencies
		Release: Combines build with config > ReleaseId (immutable)
		Run: Runs app in execution environment
	App is 1+ stateless processes & shares nothing
	App listens on ports; avoid using (web) hosts
	Use processes for isolation; multiple for concurrency
	Processes can crash/be killed quickly & start fast
	Keep dev, staging, & prod environments similar
	Log to stdout (dev=console, prod=file & archive it)
	Deploy & run admin tasks (scripts) as processes

Containers
01) PC: Hardware not shared, Kernel not shared, System Resources (e.g., File System) not shared
02) VM: Hardware shared, Kernel not shared, System Resources (e.g., File System) not shared
03) Container: Hardware shared, Kernel shared, System Resources (e.g., File System) not shared
04) Process: Hardware shared, Kernel shared, System Resources (e.g., File System) shared
05) What is a container?
	Slices up the OS to run multiple apps on a single PC/VM
	Every container gets its own root directory, network interface, own process id
	Allows a versioned set of dependencies (components, runtimes, etc.) to run side by side with another set of dependences in an isolated runtime environment on the same PC/VM
06) Docker
	There's a client (communicates with the daemon) and server
	You can pull down Docker images from a repository (Docker Hub)
	Start and stop Docker containers in the command line
