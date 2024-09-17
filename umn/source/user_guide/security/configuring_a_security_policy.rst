:original_name: asm_01_0088.html

.. _asm_01_0088:

Configuring a Security Policy
=============================

ASM security functions include **Access Authorization**, **Peer Authentication**, **JWT Authentication** to ensure the reliable service communication.

Procedure
---------

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.

#. In the navigation pane, choose **Service Management**. In the upper right corner of the list, select the namespace that your services belong to.

#. Locate the target service and click **Security** in the **Operation** column. In the window that slides out from the right, configure access authorization and peer authentication.

   **Access Authorization**

   Access authorization controls the access to services in the mesh and determines whether a request can be sent to the current service.

   On the **Access Authorization** tab, click **Configure now**. In the displayed dialog box, click |image1| to select one or more services in a specified namespace.

   **Peer Authentication**

   Istio enables communication between service pods using the Policy Enforcement Point (PEP) tunnel between clients and servers. Peer authentication defines how traffic reaches the current service pod through the tunnel (or not through the tunnel). By default, service pods that have sidecars injected communicate with each other through tunnels. Traffic is automatically encrypted using TLS.

   On the **Peer Authentication** tab, click **Configure now**. In the displayed dialog box, select an authentication policy.

   .. table:: **Table 1** Authentication policies

      +------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter  | Description                                                                                                                                                                                                      |
      +============+==================================================================================================================================================================================================================+
      | UNSET      | If a peer authentication policy is configured for the parent scope, the service inherits the policy.                                                                                                             |
      +------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | PERMISSIVE | Traffic can be transmitted without passing through the tunnel. Workloads accept both mutual TLS and plain text traffic. By default, the mesh is configured with a peer authentication policy in PERMISSIVE mode. |
      +------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | STRICT     | Traffic is transmitted only through the tunnel because the request must be encrypted using TLS and must contain the client certificate.                                                                          |
      +------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   **JWT Authentication**

   You can configure JWT authentication on ASM. With JWT, ASM authenticates whether the access token in a request header is trusted and authorize the valid user requests.

   .. note::

      JWT authentication can be configured only for HTTP services.

   On the **JWT Authentication** tab, click **Configure now**. In the displayed dialog box, set the following parameters:

   -  **Issuer**: issuer of the JWT
   -  **Audiences**: audiences who use the JWT token to access the service. Separate audiences by commas (,). A null value indicates that the service can be accessed by any audiences.
   -  **JWKS**: JWT rule set

   For details about the principles and application examples of JWT authentication, see :ref:`JWT Authentication Principles <asm_01_0096>` and :ref:`Authenticating JWT Requests on the Ingress Gateway Using ASM <asm_01_0097>`.

.. |image1| image:: /_static/images/en-us_image_0000001374968509.png
