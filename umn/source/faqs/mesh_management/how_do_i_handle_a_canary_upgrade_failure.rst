:original_name: asm_faq_0044.html

.. _asm_faq_0044:

How Do I Handle a Canary Upgrade Failure?
=========================================

There are many reasons for a canary upgrade failure. In case of a canary upgrade failure, you can use the following solutions to handle it.

#. Failed to check custom resource definitions (CRDs) before the upgrade.

   **Solution**: New Istio version does not support some CRDs, including clusterrbacconfigs, serviceroles, servicerolebindings, and policies. If there are resources to be discarded in the current version, delete them before the upgrade.

#. Failed to check Istio gateway labels before the upgrade.

   **Solution:** Configure Istio gateway labels (specified by **matchLabels**) in *{app: istio-ingressgateway, istio: ingressgateway}* format.

#. Failed to check add-ons before the upgrade.

   **Solution:** ASM 1.8 and later versions do not support the tracing, kiali, grafana, and prometheus add-ons. Uninstall the add-ons before the upgrade. You can install open-source add-ons or use APM.

#. Failed to check the cluster status before the upgrade.

   **Solution:** If the cluster is unavailable before the upgrade, do not perform the upgrade.

#. Failed to query resources before the upgrade.

   **Solution:** Prepare the required resources for the canary upgrade.

#. Failed to check the cluster version before the upgrade.

   **Solution**: Use the cluster version listed in the following table.

   ============ =========================
   Mesh Version Supported Cluster Version
   1.15         1.21,1.23,1.25,1.27
   1.18         1.25,1.27,1.28,1.29
   ============ =========================

#. Failed to check the component affinity before the upgrade.

   **Solutions**: If you upgrade Istio from a non-canary version to a canary version, ensure that there are at least twice as many nodes labeled with **istio:master** as there are istiod instances, and at least twice as many schedulable nodes as there are istio-ingressgateway or istio-egressgateway instances (depending on which one is larger). If such conditions are not met, add nodes to meet the scheduling requirements or set the anti-affinity of istiod, istio-ingressgateway, and istio-egressgateway to **Preferred**.

   -  Method 1: Add nodes labeled with **istio:master** on the CCE console.

   -  **Solution 2**: Edit the YAML file to modify the anti-affinity policy on the CCE console.

   .. code-block::

      preferredDuringSchedulingIgnoredDuringExecution:
        - weight: 1
          podAffinityTerm:
            labelSelector:
              matchExpressions:
                  - key: app
                    operator: In
                    values:
                      - istiod (For the anti-affinity policy of istio-ingressgateway, replace the value of values with istio-ingressgateway. For the anti-affinity policy of istio-egressgateway, replace the value of values with istio-egressgateway.)
             namespaces:
               - istio-system
             topologyKey: kubernetes.io/hostname

   Alternatively, change the anti-affinity from **Required** to **Preferred** on the CCE console.

#. Failed to check the automatic namespace injection before the upgrade.

   **Solution:** If there are pods in the namespace when you migrate mesh data from the Dedicated edition to the Basic edition, enable automatic injection for the namespace.
