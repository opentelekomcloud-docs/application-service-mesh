:original_name: asm_productdesc_0012.html

.. _asm_productdesc_0012:

Service Traffic Management
==========================

Application Scenarios
---------------------

Traffic management entails a wide range of operations, including:

-  Dynamically modifying load balancing policies for cross-service access, such as configuring consistent hashing to send traffic to specific service pods
-  Distributing a certain proportion of traffic to a specific version of a service when the service has two online versions
-  Protecting services, for example, limiting the number of concurrent connections and requests, and isolating faulty service pods
-  Dynamically modifying the content of a service or simulating a service running fault

Product Benefits
----------------

No code refactoring is required when you use ASM to manage traffic.

Non-intrusive traffic management capabilities are provided based on Istio. Policy- and scenario-based network connection management is provided to suit different service protocols. Different management rules can be configured for different service APIs on the topology to meet your service requirements.

Product Advantages
------------------

-  **Retry:** Auto retries upon service access failures improve the access quality and success rate. You can set the number of HTTP retry times, retry timeout duration, and retry condition.
-  **Timeout:** Auto processing and quickly failure return upon service access timeout eliminate resource locking and request freezing. You can set the HTTP request timeout duration.
-  **Connection pool management**: You can configure the maximum TCP connections, connection timeout duration, maximum non-responses, minimum idle period, and health check interval for layer-4 protocols, and configure the maximum number of HTTP requests, maximum number of retry times, maximum number of pending requests, maximum number of requests for each connection, and maximum connection idle period for layer-7 protocols. In this way, the failure of a service will not cascade and affect the entire application.
-  **Outlier detection**: You can configure the number of consecutive errors allowed before pod eviction, eviction interval, minimum eviction time, and maximum eviction ratio as outlier detection. In this way, you can check the running status of service pods on a regular basis. If access exceptions occur frequently, the pod is marked as abnormal and isolated accordingly. No traffic will be distributed to it in a specific period of time. After the isolation time, requests will be distributed to the pod. If the pod still runs abnormally, it will be isolated for a longer time. This is how pod isolation and automatic fault recovery work.
-  **Load balancing**: Diverse load balancing policies, such as random, round robin, and least connection, are provided. You can configure consistent hashing to send traffic to specific service pods.
-  **HTTP header:** You can flexibly add, edit, and remove HTTP headers, including the operations on the HTTP headers before the request is forwarded to the destination service and before the response is returned to the client.
-  **Fault injection**: Abort and delay faults can be injected to specified services to test their resilience. No code refactoring is required.
