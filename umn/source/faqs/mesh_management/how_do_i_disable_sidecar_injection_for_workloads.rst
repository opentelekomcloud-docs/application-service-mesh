:original_name: asm_faq_0037.html

.. _asm_faq_0037:

How Do I Disable Sidecar Injection for Workloads?
=================================================

If sidecar injection is enabled for a namespace of a cluster, sidecars are automatically injected for the pods of all workloads in the namespace. To prevent sidecars from being injected for some workloads, perform the following operations:

#. Log in to the CCE console and click the cluster name to go to the cluster console. In the navigation pane, choose **Workloads**. Then, click the **Deployments** tab.

#. Locate the workload and click **Edit YAML** in the **Operation** column.

#. Locate the target field based on the service mesh version and add **sidecar.istio.io/inject: 'false'**.

   -  For service meshes earlier than 1.13

      Locate the **spec.template.metadata.annotations** field and add **sidecar.istio.io/inject: 'false'**.

      .. code-block::

               annotations:
                 sidecar.istio.io/inject: 'false'

      |image1|

   -  For service meshes 1.13 or later:

      Locate the **spec.template.metadata.label** field and add **sidecar.istio.io/inject: 'false'**.

      .. code-block::

               label:
                 sidecar.istio.io/inject: 'false'

      |image2|

   For more details about sidecar injection, see `Automatic Sidecar Injection <https://istio.io/latest/docs/setup/additional-setup/sidecar-injection/#controlling-the-injection-policy>`__.

.. |image1| image:: /_static/images/en-us_image_0000001223579300.png
.. |image2| image:: /_static/images/en-us_image_0000002373720729.png
