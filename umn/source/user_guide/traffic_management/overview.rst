:original_name: asm_01_0049.html

.. _asm_01_0049:

Overview
========

Non-intrusive traffic management is a core function of Istio. With traffic management, you only need to focus on your own service logic rather than service access management. Traffic management enables you to:

-  Dynamically modify load balancing policies for cross-service access, such as configuring consistent hashing to forward traffic to specific service pods.
-  Distribute a certain proportion of traffic to a specific version of a service when the service has two online versions.
-  Protect services, for example, limiting the number of concurrent connections and requests, and isolating faulty service pods.
-  Dynamically modify the content of a service or simulate a service running fault.

ASM provides retry, timeout, connection pool, outlier detection, load balancing, HTTP header, and fault injection functions to meet traffic management requirements in most service scenarios.

.. table:: **Table 1** Common mesh functions and management roles

   ====================== ================= ================
   Mesh Function          Management Role
   \                      Service Initiator Service Provider
   Route management       Y                 N
   Load balancing         Y                 N
   Tracing analysis       Y                 Y
   Service authentication Y                 Y
   Observability data     Y                 Y
   Retry                  Y                 N
   Rewrite                Y                 N
   Redirection            Y                 N
   Authorization          N                 Y
   Fault injection        Y                 N
   Timeout                Y                 N
   Connection pool        Y                 N
   Outlier detection      Y                 N
   HTTP header            Y                 N
   ====================== ================= ================

Constraints
-----------

Traffic management cannot be performed for the service whose configuration diagnosis fails. For details about rectifying faults, see :ref:`Manual Fixing Items <asm_01_0060>` or :ref:`Auto Fixing Items <asm_01_0065>`.
