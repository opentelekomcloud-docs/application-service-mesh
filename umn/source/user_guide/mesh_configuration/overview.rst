:original_name: asm_01_0039.html

.. _asm_01_0039:

Overview
========

Mesh configuration provides cluster management, sidecar management, Istio resource management, and upgrade capabilities.

The mesh control plane workloads inject and manage sidecars of data plane pods, deliver policies and configurations, and collect monitoring data. Sidecars work with service containers in data plane pods, and they are in charge of routing and forwarding, traffic policy configuration, and monitoring data collection.

The functions of each tab page in **Mesh Configuration** are as follows:

-  **Basic Information**: You can view the mesh name, ID, status, edition, version, observability, creation time, and clusters with the mesh enabled.
-  **Sidecar Management**: You can view information about all workloads injected with sidecars, perform sidecar injection, and configure sidecar resource limits. For details, see :ref:`Sidecar Management <asm_01_0041>`.
-  **Istio Resource Management**: You can view all Istio resources (such as VirtualService and DestinationRule), create Istio resources in YAML or JSON format, and modify existing Istio resources. For details, see :ref:`Istio Resource Management <asm_01_0091>`.
-  **Upgrade**: You can upgrade the version of a service mesh.
-  Mesh extension: provides the observability configuration. For details, see :ref:`Service Mesh Extension <asm_01_0123>`.
