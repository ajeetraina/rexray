# What is Rex-Ray?

- REX-Ray is an open source, storage management solution designed to support container runtimes such as Docker and Mesos. 
- REX-Ray enables stateful applications, such as databases, to persist and maintain its data after the life cycle of the container has ended. 
- Built-in high availability enables orchestrators such as Docker Swarm, K8s, and Mesos Frameworks like Marathon to automatically orchestrate storage tasks between hosts in a cluster.

# What makes Rex-Ray a vendor agnostic model?

- RexRay is built on top of the libStorage framework. 
- LibStorage provides a vendor agnostic storage orchestration model, API, and reference client and server implementations.
- LibStorage enables storage consumption by leveraging methods commonly available, locally and/or externally, to an operating system (OS).

# Libstorage sounds interesting. Tell me more !!

- LibStorage focuses on adding value to container runtimes and storage orchestration tools such as Docker and Mesos, 
however the libStorage framework is available abstractly for more general usage across:

- Operating systems
- Storage platforms
- Hardware platforms
- Virtualization platforms

The client side implementation, focused on operating system activities, has a minimal set of dependencies in order to avoid a large, 
runtime footprint. It is imporant to note that embedding libStorage client and server components enable container runtimes to communicate directly with storage platforms, the ideal architecture.
This design requires minimal operational dependencies and is still able to provide volume management for container runtimes.

Refer [this](https://github.com/ajeetraina/rexray/libstorage/concept.md) to deep dive into architecture.

# What is CSI? Does RexRay support CSI?

The Container Storage Interface (CSI) specification is an industry-wide collaboration between the companies that make container orchestration platforms such as Kubernetes, Mesos, and Docker.Container Storage Interface (CSI), the community has cemented the role of storage and volumes with applications. This enables storage platforms and tools to focus and create trusted integrations to universally support persistent applications

REX-Ray supports CSI and adheres to all of the specification's requirements, such as idempotency. This means that all existing storage providers support CSI and are idempotent as well. Not only that, but REX-Ray supports native CSI plug-ins!

REX-Ray provided important early validation to the CSI specification by releasing initial support in 0.10. The upcoming REX-Ray 0.12 release will include CSI 0.1 support for all existing storage drivers and any new native CSI drivers.








