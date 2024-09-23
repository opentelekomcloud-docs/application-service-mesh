:original_name: asm_01_0063.html

.. _asm_01_0063:

All Pods Have Sidecars Injected
===============================

Description
-----------

An **istio-proxy** container must exist in all pods of a Service. Otherwise, this item is abnormal.

Rectification Guide
-------------------

#. Log in to the ASM console and click the name of the service mesh that the Service is added to. Choose **Mesh Configuration** in the navigation pane, click the **Sidecar Management** tab, and check whether a sidecar is injected into the namespace that the Service belongs to.

   -  If no, go to :ref:`2 <asm_01_0063__li1665121115612>`.
   -  If yes, go to :ref:`3 <asm_01_0063__li127525055610>`.

#. .. _asm_01_0063__li1665121115612:

   Inject a sidecar.

   You can inject sidecars for pods of all workloads in the namespace. For details, see :ref:`Injecting a Sidecar <asm_01_0041__section65931513505>`. You can also inject sidecars for a workload as follows:

   a. Label the namespace where the workload is located with **istio-injection=enabled**.

      **kubectl label ns** <namespace> **istio-injection=enabled**

   b. Add the **annotations** field for the workload on the CCE console.

      .. code-block::

               annotations:
                 sidecar.istio.io/inject: 'true'

      |image1|

   For more details about sidecar injection, see `Installing the Sidecar <https://istio.io/latest/docs/setup/additional-setup/sidecar-injection/>`__.

#. .. _asm_01_0063__li127525055610:

   If namespace injection is enabled for the cluster but no sidecar is injected into the pod, you need to manually restart the pod on the CCE console as follows:

   On the CCE console, choose **More** > **Redeploy** in the **Operation** column of the target workload.

#. Check whether the host network mode is configured for the workload as follows:

   On the CCE console, choose **More** > **Edit YAML** in the **Operation** column of the target workload, and check whether **spec.template.spec.hostNetwork: true** is configured. If yes, check whether this field can be deleted or set to **false**. Otherwise, sidecars cannot be injected.

   |image2|

#. Check whether the number of pods exceeds the service mesh scale.

   If the number exceeds , the excess pods cannot be injected with sidecars.

.. |image1| image:: /_static/images/en-us_image_0000001394586873.png
.. |image2| image:: /_static/images/en-us_image_0000001344069664.png
