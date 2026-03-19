:original_name: asm_01_0146.html

.. _asm_01_0146:

Using IAM Identity Policies to Grant Access to ASM
==================================================

System-defined permissions in provided by `Identity and Access Management (IAM) <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0026.html>`__ let you control access to ASM. With IAM, you can:

-  Create IAM users or user groups for personnel based on your enterprise's organizational structure. Each IAM user has their own identity credentials for accessing ASM resources.
-  Grant users only the permissions required to perform a given task based on their job responsibilities.
-  Entrust an account or a cloud service to perform efficient O&M on your ASM resources.

If your account meets your permissions requirements, you can skip this section.

:ref:`Figure 1 <asm_01_0146__en-us_topic_0000001543558165_fig1351611812271>` shows the process flow of identity policy-based authorization.

Prerequisites
-------------

Before granting permissions, learn about system-defined permissions in . To grant permissions for other services, learn about all `permissions <https://docs.otc.t-systems.com/permissions/index.html>`__ supported by IAM.

Process Flow
------------

.. _asm_01_0146__en-us_topic_0000001543558165_fig1351611812271:

.. figure:: /_static/images/en-us_image_0000002526896571.png
   :alt: **Figure 1** Process of granting ASM permissions using identity policy-based authorization

   **Figure 1** Process of granting ASM permissions using identity policy-based authorization

#. On the IAM console, .

   Create a user or user group on the IAM console.

#. (**ASMReadOnlyPolicy** as an example) to the user or user group.

#. `Log in as the IAM user <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0032.html>`__ and verify permissions.

   In the authorized region, perform the following operations:

   -  Choose **Service List** > **Application Service Mesh**. Click **Buy Mesh** on the ASM console. If a message appears indicating that you have insufficient permissions to perform the operation, **ASMReadOnlyPolicy** is in effect.
   -  Choose another service from **Service List**. If a message appears indicating that you have insufficient permissions to access the service, **ASMReadOnlyPolicy** is in effect.

Example Custom Identity Policies
--------------------------------

You can create custom identity policies to supplement the system-defined identity policies of ASM. For details about actions supported in custom identity policies, see .

To create a custom identity policy, choose either visual editor or JSON.

-  Visual editor: Select cloud services, actions, resources, and request conditions. This does not require knowledge of policy grammar.
-  JSON: Create a JSON policy or edit an existing one.

For details, see .

When creating a custom identity policy, use the Resource element to specify the resources the identity policy applies to and use the Condition element (service-specific condition keys) to control when the identity policy is in effect. For details about the supported resource types and condition keys, see .

The following provides examples of custom ASM identity policies.

-  Example 1: Grant permissions to create service meshes.

   .. code-block::

      {
          "Version": "5.0",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "asm:mesh:create",
                      "asm:mesh:createGateway"
                  ]
              }
          ]
      }

-  Example 2: Create a custom identity policy containing multiple actions.

   A custom identity policy can contain the actions of one or more services. Example identity policy containing multiple actions:

   .. code-block::

      {
          "Version": "5.0",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "asm:mesh:create",
                      "asm:mesh:createGateway"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "evs:volumes:create",
                      "evs:volumes:list"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "ecs:cloudServers:createServers",
                      "ecs:cloudServers:listServersDetails"
                  ]
              }
          ]
      }
