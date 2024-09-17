:original_name: asm_01_0069.html

.. _asm_01_0069:

The Service Is Configured with a Default-version Route and The Route Configuration Is Correct
=============================================================================================

Description
-----------

Istio defines service traffic routing rules in **VirtualService** and **DestinationRule**. Therefore, you need to configure **VirtualService** and **DestinationRule** for each service. The following rules must be met:

-  All ports of a Service must be configured in **VirtualService**.
-  The protocol type in **VirtualService** must be the same as that of the ports of a Service.
-  The default service version must be configured in **VirtualService** and **DestinationRule**.

.. note::

   If the check result changes, the port number or port name of a Service may be changed.

Rectification Guide
-------------------

#. Log in to the ASM console. Select the mesh where the service is located. In the navigation pane on the left, choose **Mesh Configuration**, click **Istio Resource Management**, and select **Istio resources: virtualservices** and the namespace to which the service belongs.

#. Ensure that all ports of the Service are configured in **VirtualService**.

   |image1|

#. Ensure that the protocol type in **VirtualService** is the same as that of the ports of the Service.


   .. figure:: /_static/images/en-us_image_0000001201436796.png
      :alt: **Figure 1** Protocol type in VirtualService

      **Figure 1** Protocol type in VirtualService


   .. figure:: /_static/images/en-us_image_0000001246196675.png
      :alt: **Figure 2** Port protocol type of the Service

      **Figure 2** Port protocol type of the Service

.. |image1| image:: /_static/images/en-us_image_0000001201276836.png
