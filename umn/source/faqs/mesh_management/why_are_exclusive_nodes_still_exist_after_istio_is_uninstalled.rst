:original_name: asm_faq_0022.html

.. _asm_faq_0022:

Why Are Exclusive Nodes Still Exist After Istio Is Uninstalled?
===============================================================

Symptom
-------

After Istio is uninstalled, exclusive nodes still exist.

Analysis
--------

Only Istio control plane workloads will be deleted when you uninstall Istio for a cluster. Node resources will not be deleted automatically.

Solution
--------

Nodes from which Istio are uninstalled can be used as common nodes. If these nodes are no longer required, log in to the CCE console and click the cluster name to go to the cluster console. Then, choose **Nodes** > **Nodes** to delete the nodes.
