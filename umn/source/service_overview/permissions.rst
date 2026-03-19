:original_name: asm_productdesc_0019.html

.. _asm_productdesc_0019:

Permissions
===========

If you need to grant your enterprise personnel permission to access your ASM resources, use Identity and Access Management (IAM). IAM provides identity authentication, fine-grained permissions management, and access control. IAM helps you secure access to your cloud resources. If your cloud account does not require individual IAM users for permissions management, you can skip this section.

IAM is a free service. You only pay for the resources in your account.

With IAM, you can control access to specific cloud resources. For example, if you want some software developers in your enterprise to be able to use ASM resources but do not want them to delete service meshes or perform any other high-risk operations, you can create IAM users and grant permission to use service meshes but not permission to delete them.

IAM supports role/policy-based authorization and identity policy-based authorization.

The following table describes the differences between these two authorization models.

.. table:: **Table 1** Differences between role/policy-based and identity policy-based authorization

   +---------------------+-------------------------------------+-------------------------------------+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Authorization Model | Core Relationship                   | Permissions                         | Authorization Method                         | Scenario                                                                                                                                                                                                                                                                                                                   |
   +=====================+=====================================+=====================================+==============================================+============================================================================================================================================================================================================================================================================================================================+
   | Role/Policy         | User-permission-authorization scope | -  System-defined roles             | Assigning roles or policies to principals    | To authorize a user, you need to add it to a user group first and then specify the scope of authorization. It provides a limited number of condition keys and cannot meet the requirements of fine-grained permissions control. This method is suitable for small- and medium-sized enterprises.                           |
   |                     |                                     | -  System-defined policies          |                                              |                                                                                                                                                                                                                                                                                                                            |
   |                     |                                     | -  Custom policies                  |                                              |                                                                                                                                                                                                                                                                                                                            |
   +---------------------+-------------------------------------+-------------------------------------+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Identity policy     | User-policy                         | -  System-defined identity policies | -  Assigning identity policies to principals | You can authorize a user by attaching an identity policy to it. User-specific authorization and a variety of key conditions allow for more fine-grained permissions control. However, this model can be hard to set up. It requires a certain amount of expertise and is suitable for medium- and large-sized enterprises. |
   |                     |                                     | -  Custom identity policies         | -  Attaching identity policies to principals |                                                                                                                                                                                                                                                                                                                            |
   +---------------------+-------------------------------------+-------------------------------------+----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Policies/identity policies and actions in the two authorization models are not interoperable. You are advised to use the identity policy-based authorization model. For details about system-defined permissions, see :ref:`Role/Policy-based Authorization <asm_productdesc_0019__en-us_topic_0000001490017126_section18155510471>` and :ref:`Identity Policy-based Authorization <asm_productdesc_0019__en-us_topic_0000001490017126_section21146354818>`.

For more information about IAM, see `IAM Service Overview <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0026.html>`__.

.. _asm_productdesc_0019__en-us_topic_0000001490017126_section18155510471:

Role/Policy-based Authorization
-------------------------------

ASM supports role/policy-based authorization. New IAM users do not have any permissions assigned by default. You need to first add them to one or more groups and then attach policies or roles to these groups. The users then inherit permissions from the groups and can perform specified operations on cloud services based on the permissions they have been assigned.

ASM is a project-level service deployed for specific regions. When you set **Scope** to **Region-specific projects** and select the specified projects in the specified regions , the users only have permissions for service meshes in the selected projects. If you set **Scope** to **All resources**, the users have permissions for service meshes in all region-specific projects. When accessing ASM, the users need to switch to the authorized region.

:ref:`Table 2 <asm_productdesc_0019__en-us_topic_0000001490017126_table8486434381>` lists all the system-defined permissions for ASM. System-defined policies in role/policy-based authorization are not interoperable with those in identity policy-based authorization.

.. _asm_productdesc_0019__en-us_topic_0000001490017126_table8486434381:

.. table:: **Table 2** System-defined permissions for ASM

   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+--------------+
   | Role/Policy Name   | Description                                                                                                                                                                                                     | Type                  | Dependencies |
   +====================+=================================================================================================================================================================================================================+=======================+==============+
   | ASM FullAccess     | Administrator permissions for ASM. Users with these permissions can perform all operations on service meshes and all resources (such as Services, gateways, and grayscale release tasks) in the service meshes. | System-defined policy | None         |
   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+--------------+
   | ASM ReadOnlyAccess | Read-only permissions for ASM. Users with these permissions can only view service meshes and all resources in the service meshes.                                                                               | System-defined policy | None         |
   +--------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+--------------+

:ref:`Table 3 <asm_productdesc_0019__en-us_topic_0000001490017126_table12985122891519>` lists the common operations supported by system-defined permissions for ASM.

.. _asm_productdesc_0019__en-us_topic_0000001490017126_table12985122891519:

.. table:: **Table 3** Common operations supported by system-defined permissions

   +-------------------------------------------------------------+----------------+--------------------+
   | Operation                                                   | ASM FullAccess | ASM ReadOnlyAccess |
   +=============================================================+================+====================+
   | Creating a service mesh                                     | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a service mesh                                     | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the service mesh list                              | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the details about a service mesh                   | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Updating a service mesh                                     | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Upgrading a service mesh                                    | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying and validating the Service of a service mesh       | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the Service list of a service mesh                 | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Repairing the Service of a service mesh with just one click | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Creating a service governance policy for a service mesh     | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the service governance policy of a service mesh    | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting the service governance policy of a service mesh    | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Obtaining the namespace list                                | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Injecting sidecars for a namespace                          | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Creating a grayscale release task                           | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a grayscale release task                           | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the grayscale release task list                    | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the details about a grayscale release task         | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Updating a grayscale release task                           | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Creating a gateway                                          | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the gateway list                                   | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a gateway                                          | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Adding a gateway route                                      | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the gateway route list                             | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a gateway route                                    | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Creating a one-click experience task                        | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the details about a one-click experience task      | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a one-click experience task                        | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the service mesh topology                          | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+

Role/Policy Dependencies of the ASM Console
-------------------------------------------

.. table:: **Table 4** Role/Policy dependencies of the ASM console

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------+
   | Console Function      | Dependency            | Role/Policy Required                                                                                                 |
   +=======================+=======================+======================================================================================================================+
   | Tracing               | APM                   | -  To enable the tracing service provided by APM 2.0, an IAM user must be granted the **APMFullAccess** permissions. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------+

.. _asm_productdesc_0019__en-us_topic_0000001490017126_section21146354818:

Identity Policy-based Authorization
-----------------------------------

ASM supports identity policy-based authorization. :ref:`Table 5 <asm_productdesc_0019__en-us_topic_0000001490017126_table056843054113>` lists all the system-defined identity policies for ASM. System-defined policies in identity policy-based authorization are not interoperable with those in role/policy-based authorization.

.. _asm_productdesc_0019__en-us_topic_0000001490017126_table056843054113:

.. table:: **Table 5** System-defined identity policies for ASM

   +----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   | Identity Policy Name | Description                                                                                                                                                                                                     | Type                           |
   +======================+=================================================================================================================================================================================================================+================================+
   | ASMFullAccess        | Administrator permissions for ASM. Users with these permissions can perform all operations on service meshes and all resources (such as Services, gateways, and grayscale release tasks) in the service meshes. | System-defined identity policy |
   +----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   | ASMReadOnlyAccess    | Read-only permissions for ASM. Users with these permissions can only view service meshes and all resources in the service meshes.                                                                               | System-defined identity policy |
   +----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+

:ref:`Table 6 <asm_productdesc_0019__table1782184143>` lists the common operations supported by system-defined identity policies for ASM.

.. _asm_productdesc_0019__table1782184143:

.. table:: **Table 6** Common operations supported by system-defined policies

   +-------------------------------------------------------------+----------------+--------------------+
   | Operation                                                   | ASM FullAccess | ASM ReadOnlyAccess |
   +=============================================================+================+====================+
   | Creating a service mesh                                     | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a service mesh                                     | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the service mesh list                              | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the details about a service mesh                   | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Updating a service mesh                                     | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Upgrading a service mesh                                    | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying and validating the Service of a service mesh       | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the Service list of a service mesh                 | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Repairing the Service of a service mesh with just one click | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Creating a service governance policy for a service mesh     | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the service governance policy of a service mesh    | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting the service governance policy of a service mesh    | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Obtaining the namespace list                                | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Injecting sidecars for a namespace                          | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Creating a grayscale release task                           | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a grayscale release task                           | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the grayscale release task list                    | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the details about a grayscale release task         | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Updating a grayscale release task                           | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Creating a gateway                                          | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the gateway list                                   | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a gateway                                          | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Adding a gateway route                                      | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the gateway route list                             | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a gateway route                                    | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Creating a one-click experience task                        | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the details about a one-click experience task      | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Deleting a one-click experience task                        | Y              | x                  |
   +-------------------------------------------------------------+----------------+--------------------+
   | Querying the service mesh topology                          | Y              | Y                  |
   +-------------------------------------------------------------+----------------+--------------------+

Identity Policy Dependencies of the ASM Console
-----------------------------------------------

.. table:: **Table 7** Identity policy dependencies of the ASM console

   +------------------+------------+-------------------------------------------------------------------------------------------------------------------+
   | Console Function | Dependency | Identity Policy Required                                                                                          |
   +==================+============+===================================================================================================================+
   | Tracing          | APM        | To enable the tracing service provided by APM 2.0, an IAM user must be granted the **APMFullAccess** permissions. |
   +------------------+------------+-------------------------------------------------------------------------------------------------------------------+

Helpful Links
-------------

-  `IAM Service Overview <https://docs.otc.t-systems.com/usermanual/iam/iam_01_0026.html>`__
-
-
