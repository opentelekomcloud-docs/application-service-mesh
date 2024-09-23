:original_name: asm_01_0057.html

.. _asm_01_0057:

Adding a Route
==============

Scenario
--------

You can add multiple routes and configure multiple forwarding policies for a created gateway.

Procedure
---------

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.
#. In the navigation pane on the left, choose **Gateway Management**, select the target gateway, click **Add Route** in the **Operation** column, and configure the following parameters:

   -  **Domain Name**

      Enter the external domain name of the service. If this parameter is left blank, the IP address of the load balancer is used by default. If you enable TLS termination, enter a domain name configured in the certificate for SNI domain name verification.

   -  **URL Matching Rule**

      -  **Prefix**: A URL can be accessed if its prefix is the same as that you configure. For example, **/healthz/v1** and **/healthz/v2**.
      -  **Exact**: Only the URL that fully matches the values you set can be accessed. For example, if the URL is set to **/healthz**, only **/healthz** can be accessed.

   -  **URL**

      Mapping URL supported by the service, for example, **/example**.

      .. note::

         The URLs of the same gateway must be unique.

   -  **Namespace**

      Select the namespace to which the gateway belongs.

   -  **Target Service**

      Service of the gateway. Select a value from the drop-down list box. The target service is filtered based on the corresponding gateway protocol. For details about the filtering rules, see :ref:`Why Cannot I Select the Corresponding Service When Adding a Route? <asm_faq_0035>`.

      The service which configuration diagnosis fails cannot be selected. You need to fix the issues first. For details, see :ref:`Manual Fixing Items <asm_01_0060>` or :ref:`Auto Fixing Items <asm_01_0065>`.

   -  **Access Port**

      Only ports that match external protocols are displayed.

   -  **Rewrite**

      (This parameter is configurable when the external protocol is HTTP.)

      Rewrite the HTTP URI and host/authority header before forwarding. Disabled by default. To enable it, configure the following parameters:

      -  URI: This value is used to rewrite the URI or prefix.
      -  Host/Authority Header: This value is used to rewrite the HTTP host/authority header.

#. Click **OK**.
