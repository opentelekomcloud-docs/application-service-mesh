:original_name: asm_faq_0031.html

.. _asm_faq_0031:

Why Does a Service Mesh Remain in the Unready Status for a Long Time After I Uninstall It?
==========================================================================================

Symptom
-------

On the ASM console, after I uninstall a service mesh, the mesh remains in the unready status for a long time.

Fault Diagnosis
---------------

#. Log in to the CCE console. Click the cluster name to go to the cluster console. In the navigation pane on the left, choose **App Templates**.

#. Click **Releases** and select the target cluster from the drop-down list. Check the releases and the latest events about uninstallation failure.

   The **Status** of **istio-master** is **Uninstallation Failed**, and the following message is displayed.

   .. code-block::

      deletion failed with 1 error(s): clusterroles:rbac.authorization.k8s.io "istio-cleanup-secrets-istio-system" already exists

Analysis
--------

Abnormal operations cause the Helm chart of Istio stuck during uninstallation. Residual resources lead to an uninstallation failure.

Solution
--------

#. Connect to the CCE cluster using kubectl.

#. Run the following commands to clear Istio resources:

   .. code-block::

      kubectl delete ServiceAccount -n istio-system `kubectl get ServiceAccount -n istio-system | grep istio | awk '{print $1}'`
      kubectl delete ClusterRole -n istio-system `kubectl get ClusterRole -n istio-system | grep istio | awk '{print $1}'`
      kubectl delete ClusterRoleBinding -n istio-system `kubectl get ClusterRoleBinding -n istio-system | grep istio | awk '{print $1}'`
      kubectl delete job -n istio-system `kubectl get job -n istio-system | grep istio | awk '{print $1}'`
      kubectl delete crd -n istio-system `kubectl get crd -n istio-system | grep istio | awk '{print $1}'`
      kubectl delete mutatingwebhookconfigurations -n istio-system `kubectl get mutatingwebhookconfigurations -n istio-system | grep istio | awk '{print $1}'`

#. Log in to the ASM console and uninstall the mesh again.
