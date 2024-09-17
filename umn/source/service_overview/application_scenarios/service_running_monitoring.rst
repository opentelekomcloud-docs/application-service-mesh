:original_name: asm_productdesc_0014.html

.. _asm_productdesc_0014:

Service Running Monitoring
==========================

Application Scenarios
---------------------

Container-based infrastructure brings a series of new challenges. It is necessary to evaluate and enhance the performance of API endpoints and identify potential risks of infrastructure. Istio service mesh enables you to enhance API performance with no code refactoring and service delay.

Product Benefits
----------------

ASM generates detailed telemetry for all service communications within the mesh. It provides observability of service behaviors and allows operators to easily troubleshoot, maintain, and optimize their applications. With ASM, operators can better understand how services interact with other services and their components.

Product Advantages
------------------

-  **Non-intrusive collection of monitoring data**: To manage and troubleshoot a complex application, it is important to obtain its access topology between services and monitoring data. ASM collects the monitoring data in a non-intrusive way. It allows you to focus on service development rather than the generation of monitoring data.
-  **Flexible service running management**: You can view the health status and dependencies between services using the access data in a topology. The topology allows you to unfold a service and observe the running status of each version of the service and each pod of a version. This pod-level topology enables you to observe how outlier detection policies work, for example, how a pod is isolated and how it recovers. When the pod is isolated, no requests are distributed to it. After it runs normally, requests are automatically distributed to it again.
