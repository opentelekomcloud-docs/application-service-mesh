:original_name: asm_faq_0037.html

.. _asm_faq_0037:

How Do I Disable Sidecar Injection for Workloads?
=================================================

After sidecar injection is enabled for a namespace of a cluster, sidecars are automatically injected for pods of all workloads in the namespace. You can configure sidecars not to be injected into some workloads:

#. Log in to the CCE console and click the cluster name to go to the cluster console. Then, choose **Workloads** > **Deployments**.

#. Locate the workload and click **Edit YAML** in the **Operation** column.

#. Find the **spec.template.metadata.annotations** field and add **sidecar.istio.io/inject: 'false'**.

   .. code-block::

            annotations:
              sidecar.istio.io/inject: 'false'

   |image1|

   For more details about sidecar injection, see `Automatic Sidecar Injection <https://istio.io/latest/docs/setup/additional-setup/sidecar-injection/#controlling-the-injection-policy>`__.

.. |image1| image:: /_static/images/en-us_image_0000001223579300.png
