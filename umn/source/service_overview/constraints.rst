:original_name: asm_productdesc_0004.html

.. _asm_productdesc_0004:

Constraints
===========

Constraints on Clusters
-----------------------

Before creating a service mesh, ensure that you have an available cluster. Cluster versions and mesh versions must meet the adaptation rules listed in :ref:`Table 1 <asm_productdesc_0004__table1495413335343>`.

.. _asm_productdesc_0004__table1495413335343:

.. table:: **Table 1** Adaptation rules between ASM and cluster versions

   =========== =============================
   ASM Version Cluster Version
   =========== =============================
   1.15        v1.21, v1.23, v1.25, or v1.27
   1.18        v1.25, v1.27, or v1.28
   =========== =============================

Containers on the node running Ubuntu 22.04 in a CCE Turbo cluster cannot be added to a service mesh earlier than v1.18.

-  Ubuntu 22.04

Constraints on Service Meshes
-----------------------------

When you use service meshes for service governance, a Deployment can only match with one service to avoid abnormal grayscale release, gateway access, or other functions.
