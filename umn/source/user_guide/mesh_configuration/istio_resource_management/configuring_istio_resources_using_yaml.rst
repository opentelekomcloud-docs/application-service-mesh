:original_name: asm_01_0048.html

.. _asm_01_0048:

Configuring Istio Resources Using YAML
======================================

You can modify all Istio resources (such as VirtualService and DestinationRule) of a service in YAML or JSON format on the **Istio Resource Management** page. You can also create new Istio resources.

Modifying an Existing Istio Resource
------------------------------------

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.

#. In the navigation pane, choose **Mesh Configuration**. Then click the **Istio Resource Management** tab.

#. In the drop-down list, select the Istio resource type (for example, Istio Resources: virtualservices) and the namespace to which the resource belongs.

#. Click **Edit** in the **Operation** column. In the right pane, modify related configurations and click **OK**.

   The configuration file can be displayed in YAML or JSON format and can be downloaded to the local PC.

Creating an Istio Resource
--------------------------

#. Log in to the ASM console and click the name of the target service mesh to go to its details page.
#. In the navigation pane, choose **Mesh Configuration**. Then click the **Istio Resource Management** tab.
#. Click **Create** in the upper left corner of the list.
#. Edit the file in the right pane, or click **Import File** to upload the edited YAML or JSON file.
#. Confirm the file content and click **OK**.
