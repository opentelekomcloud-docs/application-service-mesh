:original_name: asm_faq_0030.html

.. _asm_faq_0030:

Why Does a Service Mesh Remain in the Installing Status for a Long Time After I Enable It for a Cluster?
========================================================================================================

Symptom
-------

After I create a service mesh (that is, create a Dedicated mesh) for a CCE cluster, the mesh remains in the installing status for a long time and a message is displayed, indicating that the user security group rules are successfully enabled.

Fault Diagnosis
---------------

Log in to the CCE console and click the cluster name to go to the cluster console. In the navigation pane, choose **Namespaces**. Then, check whether the **istio-system** namespace exists.

Analysis
--------

Residual **istio-system** namespaces exist.

Solution
--------

Delete the residual **istio-system** namespaces and install the mesh again.
