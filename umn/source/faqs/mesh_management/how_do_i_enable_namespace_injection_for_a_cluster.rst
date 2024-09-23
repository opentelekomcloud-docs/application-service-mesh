:original_name: asm_faq_0036.html

.. _asm_faq_0036:

How Do I Enable Namespace Injection for a Cluster?
==================================================

When injecting a sidecar to the namespace of a cluster, if the namespace injection is not enabled in the cluster, perform the following steps:

#. Connect to the cluster using kubectl.

#. Run the **kubectl get iop -nistio-system** command to query iop resources.

   -  If the following information is displayed, the iop resource exists. Go to :ref:`3 <asm_faq_0036__li202171822811>`.

      |image1|

   -  If the following information is displayed, no iop resources exist. Go to :ref:`4 <asm_faq_0036__li797012579155>`.

      |image2|

#. .. _asm_faq_0036__li202171822811:

   Run the **kubectl edit iop -nistio-system** *data-plane* command to modify the **autoInject** configuration item. In the preceding command, *data-plane* indicates the name of the iop resource queried in the previous step. Replace it with the actual value.

   .. code-block::

          global:
            defaultPodDisruptionBudget:
              enabled: true
            hub: *.*.*.*:20202/asm
            logging:
              level: default:info
            meshID: test-payment
            multiCluster:
              clusterName: test-yy
            network: test-yy-network
            proxy:
              autoInject: enabled
            remotePilotAddress: *.*.*.*
            tag: 1.8.6-r1-20220512225026

#. .. _asm_faq_0036__li797012579155:

   Run the **kubectl edit cm -nistio-system istio-sidecar-injector** command to modify the **istio-sidecar-injector** configuration item.

   .. code-block::

      data:
        config: |-
          policy: enabled

.. |image1| image:: /_static/images/en-us_image_0000001270399104.png
.. |image2| image:: /_static/images/en-us_image_0000001321081541.png
