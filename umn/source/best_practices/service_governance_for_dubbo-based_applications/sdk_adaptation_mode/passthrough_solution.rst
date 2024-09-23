:original_name: asm_bestpractice_3004.html

.. _asm_bestpractice_3004:

PASSTHROUGH Solution
====================

Introduction
------------

When the client in the SDK calls the target service by an interface, the client accesses the service name, instead of the service instance.

|image1|

Description
-----------

Cases are different based on the Dubbo protocol versions:

-  2.7.4 and later versions: Cloud Native 2.7.4 and later versions have reconstructed the service discovery model which is consistent with that of Kubernetes. Service information can be directly obtained via interfaces.
-  2.7.3 and earlier versions: The Dubbo community versions do not provide the level-2 relationship between interfaces and services. The SDK needs to maintain the mapping from interfaces to services based on the actual usage mode. For example, information such as a service name may be provided in extended information during service registration.

You can select a processing mode based on your SDK. The SDK of an earlier version can perform the following operations in the existing service registration and discovery processes:

#. Extend the definition of **Service** in the registration information. During service deployment, service metadata can be injected into the SDK as environment variables, including **appname** and **namespace**, which indicate the name and namespace of the deployed service, respectively.
#. When the service is started, the relationship between the Dubbo interface and Kubernetes service name and namespace is registered in the Registry.
#. When a client initiates an access request, the service metadata is queried by the interface according to the original service discovery process, and the corresponding service information is used to assemble an RPC request. The extended field **Attachment** is advised to be used to store the **appname** and **namespace** information in the Dubbo request.

.. |image1| image:: /_static/images/en-us_image_0000001181766534.png
