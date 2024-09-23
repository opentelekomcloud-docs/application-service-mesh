:original_name: asm_productdesc_0001.html

.. _asm_productdesc_0001:

Introduction
============

What Is Application Service Mesh?
---------------------------------

Application Service Mesh (ASM) is a non-intrusive solution for you to manage microservice lifecycle and traffic. It is compatible with the Kubernetes and Istio ecosystems and hosts a wide range of features such as load balancing, outlier detection, and fault injection. It also provides diversified built-in grayscale releases, including canary release and blue-green deployment, for one-stop, automated release.

What Is Istio?
--------------

Istio is an open platform that provides connection, protection, control, and observation functions. By providing a complete non-intrusive microservice governance solution, Istio can well resolve service network governance issues such as cloud-native service management, network connection, and security management.

With the popularization of microservices, greater challenges emerge in the basic operations and advanced O&M of the distributed microservice architecture.

At a high level, Istio helps reduce the complexity of application deployments, and eases the strain on your development teams. It is a fully open-source service mesh that can be transparently layered onto existing distributed applications. It is also a platform, including APIs that let it integrate into any logging platform, or telemetry or policy system. Istio's diverse feature set lets you successfully and efficiently run a distributed microservice architecture, and provides a unified way to secure, connect, and monitor microservices.

**Service Mesh**

The term service mesh is used to describe the network of microservices that make up applications and the interactions between applications. As a service mesh grows in size and complexity, it can become harder to understand and manage. You need to take care of basic operations, such as service discovery, load balancing, failure recovery, metrics, and monitoring. Advanced O&M includes blue-green deployment, canary release, rate limiting, access control, and end-to-end authentication.

Why Use Istio?
--------------

Istio provides behavioral insights and operational control over the service mesh as a whole, offering a complete solution to satisfy the diverse requirements of microservice applications.

Kubernetes allows you to deploy and upgrade applications, and manage running traffic. However, capabilities such as outlier detection and rate limiting are not supported. Istio, as an open platform built based on Kubernetes, provides complementary capabilities to Kubernetes in microservice governance.

You add Istio support to services by deploying a special sidecar proxy throughout your environment that intercepts all networking requests between microservices, then configure and manage Istio using its control plane functionality, which includes:

-  Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
-  Fine-grained control of traffic behavior with rich routing rules, retries, and fault injection.
-  Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.
-  Secure service-to-service communication in a cluster with strong identity-based authentication and authorization.

Istio aims to achieve scalability and meet various deployment requirements.

Features
--------

**Grayscale release**

-  Grayscale policies based on request content: You can set criteria based on request content, such as header and cookie. Only requests meeting the criteria will be distributed to the grayscale version.
-  Grayscale policies based on traffic ratio: You can set specific ratio for the traffic to be distributed to the grayscale version.
-  Canary release: Guidance will be provided to help you perform canary release on a service, including rolling out a grayscale version, observing the running and traffic of the grayscale version, configuring grayscale release policies, and diverging the traffic.
-  Blue-green deployment: Guidance will be provided to help you perform blue-green deployment on a service, including rolling out a grayscale version, observing the running of the grayscale version, observing the traffic, and switching the traffic.

**Traffic management**

-  Layer-7 connection pool management: You can set the maximum number of HTTP requests, maximum number of retry times, maximum number of pending requests, maximum number of requests for each connection, and maximum connection idle period.
-  Layer-4 connection pool management: You can set the maximum TCP connections, connection timeout duration, maximum non-responses, minimum idle period, and health check interval.
-  Outlier detection: You can configure outlier detection rules, such as the number of consecutive errors allowed before a pod is evicted, check period, base ejection time, and maximum percentage of ejected pods.
-  Retry: You can configure the number of HTTP retry times, retry timeout duration, and retry condition.
-  Timeout: You can configure the HTTP request timeout duration.
-  Load balancing: You can configure multiple load balancing policies, such as random, round robin, least connections, and consistent hashing.
-  HTTP header: You can flexibly add, edit, and remove HTTP headers, including the operations on the HTTP headers before the request is forwarded to the destination service and before the response is returned to the client.
-  Fault injection: You can configure delay and abort faults.

**Security**

-  Peer authentication: Peer authentication defines how traffic reaches the current service pod through the tunnel (or not through the tunnel). Currently, three authentication policies are supported: **UNSET**, **PERMISSIVE**, and **STRICT**.
-  Access authorization: Access authorization controls the access to services in the mesh and determines whether a request can be sent to the current service.

**Observability**

-  Application access topology: An application access topology shows the dependencies between services.
-  Service running monitoring: Service access information, including service information, different versions of the service, QPS, and latency can be monitored.
-  Access logs: Service access logs can be collected and searched.

**Framework of the mesh data plane**

-  Spring Cloud: supports unified management of services developed using Spring Cloud SDK.
-  Dubbo: supports unified management of services developed using Dubbo SDK.

**Compatibility and extension**

-  Community compatibility: ASM APIs are fully compatible with the Istio community.
-  Support for community add-ons: Tracing, Prometheus, Kiali, and Grafana are supported.
