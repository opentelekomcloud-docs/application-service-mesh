:original_name: asm_01_0063.html

.. _asm_01_0063:

All Pods Have Sidecars Injected
===============================

Description
-----------

An **istio-proxy** container must exist in all pods of a Service. Otherwise, this item is abnormal.

Rectification Guide
-------------------

#. Log in to the ASM console and click the name of the service mesh that the Service is added to. In the navigation pane, choose **Mesh Configuration**. On the displayed page, click the **Sidecar Management** tab. Then, check whether a sidecar is injected into the namespace that the Service belongs to.

   -  If the sidecar is not injected into the namespace, go to :ref:`2 <asm_01_0063__li1665121115612>`.

   -  If the sidecar has been injected into the namespace, go to :ref:`3 <asm_01_0063__li127525055610>`.

      Check method:

      On the CCE console, click the cluster name to access the cluster console. In the navigation pane, choose **Namespaces**. On the displayed page, locate your namespace and click **Edit YAML** in the **Operation** column. If there is the **istio.io/rev=<revision>** or **istio-injection=enabled** label, the sidecar has been injected.

      .. note::

         -  There must the **istio-injection=enabled** label for Istio 1.13.9-r3 and earlier versions, as well as Istio 1.15.5-r2 and earlier versions. Note that the version numbers are combined by hyphens (-).

         -  There must be the **istio.io/rev=<revision>** label for Istio later than 1.13.9-r3, Istio later than 1.15.5-r2, and all Istio 1.18 versions. Note that the version numbers are combined by hyphens (-).

            |image1|

#. .. _asm_01_0063__li1665121115612:

   Inject a sidecar into a workload or inject sidecars into the pods of all workloads in the namespace.

   Injection methods:

   -  To inject sidecars into the pods of all workloads in the namespace, run the following command to add a label to the namespace (the label varies depending on the Istio version):

      .. code-block::

         kubectl label ns <namespace> istio-injection=enabled

      Or

      .. code-block::

         kubectl label ns <namespace> istio.io/rev=<revision>

      .. note::

         The system adds labels for namespaces based on Istio versions.

         -  **istio-injection=enabled** can be used in Istio 1.13.9-r3 and earlier versions, as well as Istio 1.15.5-r2 and earlier versions.

         -  **istio.io/rev=<revision>** can be used in Istio later than 1.13.9-r3, Istio later than 1.15.5-r2, and all Istio 1.18 versions.

   -  Injecting a sidecar into a workload

      On the CCE console, locate the target workload, choose **More** > **Edit YAML** in the **Operation** column, and manually add the **annotations** or **labels** field based on your Istio version.

      -  For 1.13.9-r3 and later versions, 1.15.5-r2 and later versions, and all 1.18 versions, the configuration is follows:

         .. code-block::

                  labels:
                    istio.io/rev=<revision>

      -  For 1.13.9-r3 and earlier versions as well as 1.15.5-r2 and earlier versions, the configuration is follows:

         .. code-block::

                  annotations:
                    istio-injection: enabled

   For more details about sidecar injection, see `Installing the Sidecar <https://istio.io/latest/docs/setup/additional-setup/sidecar-injection/>`__.

#. .. _asm_01_0063__li127525055610:

   If namespace injection is enabled for the cluster but no sidecar is injected into the pod, you need to manually restart the pod on the CCE console as follows:

   On the CCE console, choose **More** > **Redeploy** in the **Operation** column of the target workload.

#. Check whether the host network mode is configured for the workload as follows:

   On the CCE console, choose **More** > **Edit YAML** in the **Operation** column of the target workload, and check whether **spec.template.spec.hostNetwork: true** is configured. If yes, check whether this field can be deleted or set to **false**. Otherwise, sidecars cannot be injected.

   |image2|

#. Check whether the number of pods exceeds the service mesh scale.

   If the number exceeds, the excess pods cannot be injected with sidecars.

.. |image1| image:: /_static/images/en-us_image_0000002086005592.png
.. |image2| image:: /_static/images/en-us_image_0000001344069664.png
