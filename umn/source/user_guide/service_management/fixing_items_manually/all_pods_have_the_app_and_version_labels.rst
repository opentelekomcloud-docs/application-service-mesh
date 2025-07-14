:original_name: asm_01_0061.html

.. _asm_01_0061:

All Pods Have the app and version Labels
========================================

Description
-----------

All pods of a Service must be labeled with **app** and **version**. **app** traces traffic in traffic monitoring, and **version** distinguishes different versions in grayscale release. If a pod is not labeled with **app** or **version**, this item is abnormal.

.. _asm_01_0061__section551915418912:

Rectification Guide
-------------------

The labels of pods are configured in **spec.template.metadata.labels** of the Deployment. The recommended configuration is as follows:

.. code-block::

   labels:
     app: {serviceName}
     version: v1

.. caution::

   Modifying or deleting the Deployment will trigger pod rolling upgrade, which may cause temporary service interruption. Therefore, perform the operation at a proper time.

#. Copy the original workload configuration and save it as a YAML file.

   **kubectl get deployment** {deploymentName} **-n** {namespace} **-o yaml >** {deploymentName}\ **-deployment.yaml**

   For example:

   **kubectl get deployment productpage -n default -o yaml > productpage-deployment.yaml**

#. Modify the **productpage-deployment.yaml** file. If the file does not contain **app** and **version**, add them. You are advised to set **app** to the Service name and the **version** to **v1**.

#. Delete the original workload.

   **kubectl delete deployment** {oldDeploymentName} **-n** {namespace}

#. Apply the new workload configuration.

   **kubectl apply -f productpage-deployment.yaml**

.. note::

   For clusters of v1.15 or earlier, you can modify pod labels on the CCE console, but residual ReplicaSets may exist.

   To check whether there are residual ReplicaSets, perform the following steps:

   #. Query the ReplicaSets of the Deployment.

      **kubectl get replicaset \| grep** {deploymentName}

   #. Find the ReplicaSets containing more than one pod. These ReplicaSets may be residual after label modification. You need to delete the old ReplicaSets.

      **kubectl delete replicaset** {replicaSetName} **-n** {namespace}
