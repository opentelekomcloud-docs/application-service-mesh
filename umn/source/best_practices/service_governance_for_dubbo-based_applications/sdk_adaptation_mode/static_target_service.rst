:original_name: asm_bestpractice_3005.html

.. _asm_bestpractice_3005:

Static Target Service
=====================

Introduction
------------

Use `dubbo:reference <https://dubbo.apache.org/en/docs/v2.7/user/references/xml/dubbo-reference/>`__ to configure the referenced service provider in the service consumer of the Dubbo service. Use the **url** option to define the address of the point-to-point direct connection service provider to bypass the Registry and directly call the target service.

Description
-----------

If the original Dubbo service uses the **.xml** configuration file, only the configuration file needs to be modified.

.. code-block::

   <?xml version="1.0" encoding="UTF-8"?>
   <beans>
       <!-- Interfaces that can be called -->
       <dubbo:reference id="helloService " interface="com.dubbo.service.HelloService " url = "dubbo://helloService:20880" />
   </beans>

If an annotation is used to define the referenced target service, only the annotation of the target service in the code needs to be modified.

.. code-block::

   @Reference(url = "dubbo://helloService:20880")
   HelloService helloService;
