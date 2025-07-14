:original_name: asm_01_0062.html

.. _asm_01_0062:

All Pods Share the Same app and version Labels
==============================================

Description
-----------

All pods of a Service must share the same **app** and **version** labels. **app** traces traffic in traffic monitoring, and **version** distinguishes different versions in grayscale release. If pods with different **app** or **version** labels exist, this item is abnormal.

Rectification Guide
-------------------

The labels of pods are configured in **spec.template.metadata.labels** of the Deployment. The recommended configuration is as follows:

.. code-block::

   labels:
     app: {serviceName}
     version: v1

To modify the labels of multiple pods to the same value, perform the following steps:

#. View the labels configured for **spec.selector**.

   **kubectl get svc** {serviceName} **-o yaml**

   For example, the labels are **app: ratings** and **release: istio-bookinfo**.

#. Search for the pods of a Service by label.

   **kubectl get pod -n** {namespace} **-l app=ratings,release=istio-bookinfo**

   .. note::

      **{namespace}** is the same as the namespace of the Service.

#. Find the workload of a pod by the pod name.

   **kubectl get deployment** {deploymentName} **-n** {namespace}

   .. note::

      -  Generally, the pod name is in the format of **{deploymentName}-{random character string}-{random character string}**.

      -  If no workload of a pod is found by the pod name, you need to delete residual ReplicaSets.

         To check whether there are residual ReplicaSets, perform the following steps:

         a. Query the ReplicaSets of the Deployment.

            **kubectl get replicaset \| grep** {deploymentName}

         b. Find the ReplicaSets containing more than one pod. These ReplicaSets may be residual after label modification. You need to delete the old ReplicaSets.

            **kubectl delete replicaset** {replicaSetName} **-n** {namespace}

#. For details about how to modify the **app** and **version** labels of a pod, see :ref:`Rectification Guide <asm_01_0061__section551915418912>`.
