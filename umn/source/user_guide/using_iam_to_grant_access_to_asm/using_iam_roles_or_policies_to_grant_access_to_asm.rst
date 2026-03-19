:original_name: asm_01_0145.html

.. _asm_01_0145:

Using IAM Roles or Policies to Grant Access to ASM
==================================================

System-defined permissions in provided by `Identity and Access Management (IAM) <https://docs.otc.t-systems.com/en-us/usermanual/iam/iam_01_0026.html>`__ let you control access to ASM. With IAM, you can:

-  Create IAM users for personnel based on your enterprise's organizational structure. Each IAM user has their own identity credentials for accessing ASM resources.
-  Grant users only the permissions required to perform a given task based on their job responsibilities.
-  Entrust an account or a cloud service to perform efficient O&M on your ASM resources.

If your account meets your permissions requirements, you can skip this section.

:ref:`Figure 1 <asm_01_0145__en-us_topic_0000001489537442_fig1351611812271>` shows the process flow of role/policy-based authorization.

Prerequisites
-------------

Before granting permissions to user groups, learn about system-defined permissions in for ASM. To grant permissions for other services, learn about all `permissions <https://docs.otc.t-systems.com/permissions/index.html>`__ supported by IAM.

Process Flow
------------

.. _asm_01_0145__en-us_topic_0000001489537442_fig1351611812271:

.. figure:: /_static/images/en-us_image_0000002526896489.png
   :alt: **Figure 1** Process of granting ASM permissions using role/policy-based authorization

   **Figure 1** Process of granting ASM permissions using role/policy-based authorization

#. .. _asm_01_0145__en-us_topic_0000001489537442_li10176121316284:

   On the IAM console, `create a user group and assign permissions to it <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0030.html>`__.

   Create a user group on the IAM console, and assign the **ASM ReadOnlyAccess** permissions to the group.

#. `Create an IAM user and add it to the user group <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0031.html>`__.

   On the IAM console, create a user and add it to the user group created in :ref:`1 <asm_01_0145__en-us_topic_0000001489537442_li10176121316284>`.

#. `Log in as the IAM user <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0032.html>`__ and verify permissions.

   In the authorized region, perform the following operations:

   -  Choose **Service List** > **Application Service Mesh**. Click **Buy Mesh** on the ASM console. If a message appears indicating that you have insufficient permissions to perform the operation, the **ASM ReadOnlyAccess** policy is in effect.
   -  Choose another service from **Service List**. If a message appears indicating that you have insufficient permissions to access the service, the **ASM ReadOnlyAccess** policy is in effect.

Example Custom Policies
-----------------------

You can create custom policies to supplement the system-defined policies of ASM. For details about actions supported in custom policies, see .

To create a custom policy, choose either visual editor or JSON.

-  Visual editor: Select cloud services, actions, resources, and request conditions. This does not require knowledge of policy grammar.
-  JSON: Create a JSON policy or edit an existing one.

For details, see .

The following lists examples of common ASM custom policies.

-  Example 1: Grant permissions to create service meshes.

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "asm:mesh:create"
                  ]
              }
          ]
      }

-  Example 2: Grant permissions to deny service mesh deletion.

   A policy with only "Deny" permissions must be used together with other policies. If the permissions granted to an IAM user contain both "Allow" and "Deny", the "Deny" permissions take precedence over the "Allow" permissions.

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Deny",
                  "Action": [
                      "asm:mesh:createGateway"
                  ]
              }
          ]
      }

-  Example 3: Create a custom policy containing multiple actions.

   A custom policy can contain the actions of one or multiple services that are of the same type (global or project-level). Example policy containing actions of multiple services:

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "cce:cluster:create"
                      "asm:mesh:create"
                  ]
              }
          ]
      }
