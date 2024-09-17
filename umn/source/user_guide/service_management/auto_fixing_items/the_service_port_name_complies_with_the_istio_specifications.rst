:original_name: asm_01_0066.html

.. _asm_01_0066:

The Service Port Name Complies with the Istio Specifications
============================================================

Description
-----------

The Service port name must contain the specified protocol and prefix and must be in the following format:

.. code-block::

   name: <protocol>[-<suffix>]

**<protocol>** can be **http**, **tcp**, or **grpc**. Istio provides routing capabilities based on protocols defined on ports. For example, **name: http-service0** and **name: tcp** are valid port names, while **name: httpforecast** is not.

If the Service port name is invalid, this item is abnormal.

Rectification Guide
-------------------

#. Log in to the CCE console.

#. Click the cluster name to go to the cluster console. In the navigation pane on the left, choose **Services & Ingresses**. On the **Services** tab, search for the Service by cluster name and namespace and click **Edit YAML**. Then, view the Service protocol and add a protocol type before the service name.

   |image1|

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001254992703.png
