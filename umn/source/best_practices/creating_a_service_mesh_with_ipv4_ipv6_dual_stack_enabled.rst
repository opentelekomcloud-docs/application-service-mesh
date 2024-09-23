:original_name: asm_bestpractice_1009.html

.. _asm_bestpractice_1009:

Creating a Service Mesh with IPv4/IPv6 Dual Stack Enabled
=========================================================

You can create a CCE cluster with IPv4/IPv6 dual stack enabled and enable IPv4/IPv6 dual stack for the service mesh that the cluster is added to. IPv4/IPv6 dual stack allows services in the service mesh to use both IPv4 and IPv6 addresses for service-to-service interactions. After an IPv4/IPv6 dual-stack gateway is added for the service mesh, you can provide services for users using an IPv6 client. This section describes how you can create a service mesh with IPv4/IPv6 dual stack, so that services in the service mesh can communicate with each other using IPv6 addresses.

Application Scenarios
---------------------

-  If an IPv6 address is required for service access and traffic management, you can enable IPv4/IPv6 dual stack.
-  If you provide services for users who use IPv6 clients, you can create a gateway for a service mesh with IPv4/IPv6 dual stack enabled.

Constraints
-----------

-  Constraints on enabling IPv4/IPv6 dual stack for a service mesh

+----------------------+---------------+--------------------+--------------------------+--------------------------------------------+
| Service Mesh Edition | Istio Version | Cluster Type       | Cluster Network Type     | Remarks                                    |
+======================+===============+====================+==========================+============================================+
| Basic                | 1.18 or later | CCE Turbo clusters | Cloud native network 2.0 | IPv6 needs to be enabled for the clusters. |
+----------------------+---------------+--------------------+--------------------------+--------------------------------------------+

-  Constraints on creating an IPv4/IPv6 dual-stack gateway

+----------------------+---------------+--------------------+----------------------------------+----------------------------------------+
| Service Mesh Edition | Istio Version | Load Balancer Type | Load Balancer Specification      | Remarks                                |
+======================+===============+====================+==================================+========================================+
| Basic                | 1.18 or later | Dedicated          | Network load balancing (Layer 4) | The load balancer has an IPv6 address. |
+----------------------+---------------+--------------------+----------------------------------+----------------------------------------+

-  IPv4/IPv6 dual stack cannot be disabled once it is enabled for a service mesh. IPv4/IPv6 dual stack cannot be enabled for an existing service mesh.
-  IPv4/IPv6 dual stack is only available for service meshes of v1.18 or later, but it cannot be enabled for a service mesh that is upgraded to v1.18 or later.

Creating a Service Mesh with IPv6 Addresses
-------------------------------------------

#. Log in to the ASM console, a service mesh, and configure the parameters as follows:

   -  **Mesh Edition**: Select **Basic edition**.
   -  **Mesh Name**: Enter a service mesh name.
   -  **Istio Version**: Select 1.18 or later.
   -  **Enable IPv6**: If this option is enabled, CCE clusters that meet the conditions will be displayed.

   Configure other parameters based on site requirements.

#. Click the service mesh name to access the details page.

   On the **Mesh Configuration** > **Basic Information** tab, you can see that IPv4/IPv6 dual stack has been enabled.

Adding an IPv4/IPv6 Dual-Stack Gateway
--------------------------------------

#. Log in to the ASM console. On the service mesh list page, click the name of the service mesh with IPv4/IPv6 dual stack enabled. In the navigation pane, choose **Gateway Management**. Click **Add Gateway** and configure the parameters as follows:

   -  **Access Mode**: Select IPv4/IPv6 dual stack.
   -  **Load Balancer**: Select **Dedicated**. The dedicated load balancer must have an IPv6 address.

   Configure other parameters based on site requirements.

   .. note::

      If IPv4/IPv6 dual stack is enabled, only domain names are allowed to access the gateway.

Verification
------------

#. Configure domain name resolution for the client, so that the domain name is mapped to the IPv6 address of the gateway. This way, the client can access the gateway using the domain name.

|image1|

2. View the IPv6 request information in the ingressgateway log.

|image2|

.. |image1| image:: /_static/images/en-us_image_0000001741270036.png
.. |image2| image:: /_static/images/en-us_image_0000001786644069.png
