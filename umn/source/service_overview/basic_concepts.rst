:original_name: asm_productdesc_0005.html

.. _asm_productdesc_0005:

Basic Concepts
==============

Workload
--------

A workload is an abstract model of a group of pods in Kubernetes. Workloads defined in Kubernetes include Deployments, StatefulSets, jobs, and DaemonSets.

-  **Deployment**: Pods of a Deployment are completely independent of each other and deliver the same functions. Deployments support auto scaling and rolling updates. Typical examples include Nginx and WordPress.
-  **StatefulSet**: Pods in a StatefulSet are not completely independent of each other. StatefulSets have stable persistent storage and unique network identifiers. They support ordered, graceful deployment, scaling, and deletion. Typical examples include MySQL-HA and etcd.

Pod
---

A pod is the smallest and simplest unit in the Kubernetes object model that you create or deploy. A pod encapsulates an application container (in some cases, multiple containers), storage resources, a unique network IP address, and options that govern how the container should run.

Canary Release
--------------

Grayscale release is essential for smooth rollout of iterative software products in production environments. A certain proportion of production traffic on the live network is distributed to a new version of the application to test the version's performance and detect faults while ensuring stable running of the system.

Blue-Green Deployment
---------------------

Blue-green deployment is a zero-downtime deployment mode. A new version of an application is deployed and tested in a production environment while the live environment continues to serve all production traffic. When you confirm that the new version is functioning properly, traffic is then distributed to the new version. At the same time, the old version is upgraded to the new version. Blue-green deployment allows you to quickly switch between the two versions to effectively prevent service disruption during the upgrade.

Traffic Management
------------------

Traffic management provides you with visualized network statuses of cloud native applications and allows you to manage and configure network connections and security policies online. Currently, it supports connection pool, outlier detection, load balancing, HTTP header, fault injection, etc.

Connection Pool Management
--------------------------

Thresholds for TCP and HTTP connections and request pools to prevent a service from overloading.

Outlier Detection
-----------------

Quick response and service access fault isolation are configured to prevent a cascade of network and service calling faults. In this way, the fault impact is curbed. The overall system performance deterioration or avalanche is prevented.
