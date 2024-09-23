:original_name: asm_productdesc_0013.html

.. _asm_productdesc_0013:

End-to-End Transparency and Security
====================================

Application Scenarios
---------------------

Splitting traditional monolithic applications into microservices brings various benefits, including better flexibility, scalability, and reusability. The new security requirements microservices have are as follows:

-  Traffic encryption is required to defend against man-in-the-middle attacks.
-  TLS and fine-grained access control policies are required for flexible service access control.
-  Audit tools are needed to determine who can do what at what time.

ASM provides a comprehensive security solution, including authentication policies, transparent TLS encryption, and authorization and audit tools, to address these requirements.

Product Benefits
----------------

-  **Default security**: No modification is required on application code and architecture to ensure security.
-  **In-depth defense**: ASM can integrate with existing security systems to provide comprehensive defense.
-  **Zero-trust network**: The security solution is built assuming that all the network is untrusted.

Product Advantages
------------------

-  **Non-intrusive security**: ASM provides service meshes as infrastructure with built-in security capabilities. It allows you to focus more on the development and O&M of your services. No code refactoring is required to ensure service access security. ASM provides a transparent, distributed security layer and underlying secure communication channels, which manage authentication, authorization, and encryption for service communication. ASM provides communication security between pods and services. Developers only need to focus on application-level security based on this security infrastructure layer.
-  **Fine-grained authorization**: After authentication, access authorization between services can be managed. Authorization management can be performed on a specific service or a specific API of a service. For example, you can authorize all services in a specific namespace or only a specific service. The source service and destination service can be in different clusters. Pods of the source service can be in different clusters. Pods of the destination service can be in different clusters.
