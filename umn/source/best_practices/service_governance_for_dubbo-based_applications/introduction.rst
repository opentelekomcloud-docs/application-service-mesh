:original_name: asm_bestpractice_3002.html

.. _asm_bestpractice_3002:

Introduction
============

Dubbo is a special protocol. The following functions must be provided:

-  Envoy on the service mesh data plane parses protocols and manages traffic of Dubbo.
-  The service mesh control plane supports Dubbo governance rules and service management such as grayscale release, load balancing, and access authorization.

In addition, the service discovery model of Dubbo is different from that of Kubernetes or Spring Cloud. Additional processing is required.
