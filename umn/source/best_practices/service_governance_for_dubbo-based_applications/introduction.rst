:original_name: asm_bestpractice_3002.html

.. _asm_bestpractice_3002:

Introduction
============

Dubbo is a special protocol which needs the following supports:

-  Envoy on the service mesh data plane supports the parsing and traffic management of the Dubbo protocol.
-  The mesh control plane supports the configuration of Dubbo governance rules to manage services such as grayscale release, load balancing, and access authorization.

In addition, the service discovery model of Dubbo is different from that of Kubernetes and Spring Cloud. Therefore, additional processing is required.
