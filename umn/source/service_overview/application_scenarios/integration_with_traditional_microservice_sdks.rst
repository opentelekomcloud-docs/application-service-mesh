:original_name: asm_productdesc_0015.html

.. _asm_productdesc_0015:

Integration with Traditional Microservice SDKs
==============================================

Application Scenarios
---------------------

-  Using service meshes to manage services developed using traditional SDKs.
-  Integrating Istio with microservice platforms and building a microservice management and control center based on Istio.

Product Benefits
----------------

Integration solutions for traditional microservice SDKs, such as Spring Cloud and Dubbo are provided. Services developed using traditional microservice SDKs can be migrated to cloud-native containers and meshes without major code modification.

Product Advantages
------------------

-  **Non-intrusive migration solution**: ASM provides a non-intrusive solution to help you migrate services developed using traditional SDKs to service meshes. The service invoker diverts outbound traffic to the mesh data plane. That is, the service discovery and load balancer in the original SDK are short-circuited. The Kubernetes service name is used for access, and the service discovery in the Kubernetes is used. The governance logic in the SDK can be gradually replaced by the mesh. In this way, the service running and governance capabilities are provided directly by the infrastructure based on Kubernetes and service meshes.
-  **Unified policy management**: The unified ASM control plane is used to discover services and manage governance rules. No independent registration center or configuration center is required. Service discovery, load balancing, and governance on the data plane are all performed using the data plane Envoy. SDKs only function as a lightweight application development framework.
-  **Multiple infrastructure resources**: In the solution, the data plane can be deployed on containers or VMs. Services can be developed in various languages. There is no restriction on the development framework. Traffic rules are delivered through the mesh control plane and all forms of data planes are managed in a unified manner.
