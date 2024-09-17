:original_name: asm_01_0056.html

.. _asm_01_0056:

Adding a Gateway
================

A gateway enables unified entry, traffic management, security, and service isolation.

Prerequisites
-------------

Gateways use load balancers of ELB to provide network access. Before adding a gateway, you need to create a load balancer.

When creating a load balancer, you need to ensure that it belongs to the same VPC as the cluster.

Procedure
---------

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.

#. In the navigation pane on the left, choose **Gateway Management** and click **Add Gateway**.

#. Configure the following parameters.

   -  **Gateway Name**

      Enter a gateway name. Enter 4 to 59 characters starting with a lowercase letter and ending with a lowercase letter or digit. Only lowercase letters, digits, and hyphens (-) are allowed.

   -  **Cluster**

      Select the cluster to which the gateway belongs.

   -  **Load Balancer**

      -  Gateways use shared load balancers of ELB for the access over both public and private IPv4 networks.

   -  **Listener**

      Gateways configure a listener for the load balancer, which listens to requests from the load balancer and distributes traffic.

      -  **External Protocol**

         Select one to match the protocol type of your service. **HTTP**, **gRPC**, **TCP**, **TLS**, and **HTTPS** are supported.

      -  **External Port**

         Enter the port number exposed in the Load Balancer Service address. The port number can be specified randomly.

      -  **TLS Termination**

         If **External Protocol** is **HTTPS**, **TLS Termination** is enabled and cannot be disabled.

         If **External Protocol** is **TLS**, you can enable or disable **TLS Termination**. If you enable TLS termination, bind a certificate to support TLS-based data transmission encryption and authentication. If you disable TLS termination, encrypted TLS data will be directly forwarded.

      -  **Secret Certificate**

         -  When configuring a TLS protocol with TLS termination enabled, you need to bind a certificate to support TLS-based data transmission encryption and authentication.
         -  When configuring the HTTPS protocol, you need to bind a secret certificate.

      -  **Earliest TLS Version Supported/Latest TLS Version Supported**

         When configuring a TLS protocol with TLS termination enabled or an HTTPS protocol, you can select the earliest and latest TLS versions.

#. (Optional) Configure routing parameters.

   When the access address of a request matches the forwarding policy (which consists of a domain name and URL. If the domain name is left empty, the ELB IP address is used by default), the request is forwarded to the corresponding target Service for processing. Click |image1|. The **Add Route** dialog box is displayed.

   -  **Domain Name**

      Enter the external domain name of the service. If this parameter is left blank, the IP address of the load balancer is used by default. If you enable TLS termination, enter a domain name configured in the certificate for SNI domain name verification.

   -  **URL Matching Rule**

      -  **Prefix**: A URL can be accessed if its prefix is the same as that you configure. For example, **/healthz/v1** and **/healthz/v2**.
      -  **Exact**: Only the URL that fully matches the values you set can be accessed. For example, if the URL is set to **/healthz**, only **/healthz** can be accessed.

   -  **URL**

      Mapping URL supported by the service, for example, **/example**.

   -  **Namespace**

      Select the namespace to which the gateway belongs.

   -  **Target Service**

      Service of the gateway. Select a value from the drop-down list box. The target service is filtered based on the corresponding gateway protocol. For details about the filtering rules, see :ref:`Why Cannot I Select the Corresponding Service When Adding a Route? <asm_faq_0035>`

      The service which configuration diagnosis fails cannot be selected. You need to fix the issues first. For details, see :ref:`Manual Fixing Items <asm_01_0060>` or :ref:`Auto Fixing Items <asm_01_0065>`.

   -  **Access Port**

      Only ports that match external protocols are displayed.

   -  **Rewrite**

      (This parameter is configurable when the external protocol is HTTP.)

      Rewrite the HTTP URI and host/authority header before forwarding. Disabled by default. To enable it, configure the following parameters:

      -  URI: This value is used to rewrite the URI or prefix.
      -  Host/Authority Header: This value is used to rewrite the HTTP host/authority header.

#. Click **OK**.

   You can obtain the external network access address of the service in the **Service Management** page.

.. |image1| image:: /_static/images/en-us_image_0000001209954130.png
