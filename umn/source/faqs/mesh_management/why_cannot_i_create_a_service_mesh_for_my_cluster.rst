:original_name: asm_faq_0020.html

.. _asm_faq_0020:

Why Cannot I Create a Service Mesh for My Cluster?
==================================================

Symptom
-------

I cannot create a service mesh for my cluster.

Analysis
--------

Currently, clusters earlier than v1.21 cannot be managed by service meshes.

Solution
--------

#. Check the cluster version. Currently, only clusters v1.21 or later can be managed by service meshes.
#. Check your browser. Chrome is recommended. The button for service mesh creation may be unavailable when you are using other browsers, such as Firefox, due to adaptation problems.
