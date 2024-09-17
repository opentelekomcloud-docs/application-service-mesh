:original_name: asm_01_0086.html

.. _asm_01_0086:

Uninstalling a Mesh
===================

Scenario
--------

When a mesh is no longer needed, you can uninstall it.

Constraints
-----------

-  To uninstall a mesh in which a grayscale release task is running, you need to complete the grayscale release first.
-  You need to ensure available nodes exist in the clusters for running the cleanup task to avoid uninstallation failure.

Procedure
---------

#. Log in to the ASM console.

#. Click |image1| in the target mesh.

#. On the dialogue box displayed, select whether to restart existing services and read the precautions.

   By default, existing services are not restarted during the uninstallation. The injected istio-poxy sidecar is removed only after the existing services are restarted. If you want to restart the services, select **Yes**. Restarting the services will interrupt your services temporarily.

   .. note::

      You are advised to restart existing services to avoid the following exceptions: If the cluster enables the current mesh again after it is uninstalled, gateway access failed.

   -  Uninstalling a mesh will uninstall its control plane components and data plane sidecars.

   -  After the uninstallation, service gateways of applications cannot be used. Configure Services for external access to applications.

      To update the external access mode, log in to the CCE console and click the cluster name to go to the cluster console. Then, choose **Services & Ingresses** > **Services**.

   -  Uninstalling a mesh will delete the labels of the mesh exclusive nodes, but the Istio-master node will not be automatically deleted. You can delete it on the CCE console.

      To view node information, log in to the CCE console and click the cluster name to go to the cluster console. In the navigation pane on the left, choose **Nodes** > **Nodes**.

.. |image1| image:: /_static/images/en-us_image_0000001255111219.png
