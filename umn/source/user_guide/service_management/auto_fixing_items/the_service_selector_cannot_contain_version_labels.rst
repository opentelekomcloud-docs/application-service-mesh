:original_name: asm_01_0067.html

.. _asm_01_0067:

The Service Selector Cannot Contain version Labels
==================================================

Description
-----------

The **spec.selector** of a Service cannot be labeled with **version**. Otherwise, this item is abnormal.

Rectification Guide
-------------------

#. Log in to the CCE console.

#. Click the cluster name to go to the cluster console. In the navigation pane on the left, choose **Services & Ingresses**. On the **Services** tab, search for the Service by cluster name and namespace and click **Edit YAML**. Then, view the selector (specified by **spec.selector**) of the Service and delete the **version** label.

   |image1|

.. |image1| image:: /_static/images/en-us_image_0000001254992865.png
