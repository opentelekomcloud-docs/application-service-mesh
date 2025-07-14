:original_name: asm_faq_0030.html

.. _asm_faq_0030:

Why Does an Enabled Service Mesh Remain in the Installing State for a Long Time?
================================================================================

Symptom
-------

After I enable a service mesh (create a service mesh) for a CCE cluster, it remains in the installing state for a long time and a message is displayed indicating that the Istio-based service mesh is being enabled and the security group rules are successfully enabled.

Fault Diagnosis
---------------

Log in to the CCE console and click the cluster name to go to the cluster console. In the navigation pane, choose **Namespaces**. Then, check whether the **istio-system** namespace exists.

Analysis
--------

Residual **istio-system** namespaces exist.

Solution
--------

Delete the residual **istio-system** namespaces and install the service mesh again.
