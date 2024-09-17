:original_name: asm_faq_0003.html

.. _asm_faq_0003:

What Do I Do If an Added Gateway Does Not Take Effect?
======================================================

The possible cause is that the Gateway-related resource configurations are missing or incorrect. Do as follows to locate the fault:

-  Log in to the Elastic Load Balance console, check whether the external port and ECSs are successfully listened by the load balancer.
-  Log in to the cluster and run the **kubectl get gateway -n istio-system** command to check whether the IP address, domain name, and port number are configured for the Gateway. Run the **kubectl get svc -n istio-system** command to check whether the ingress Gateway has the corresponding IP address and port and is not in the pending status.
-  Check whether the internal access protocol of the service added to the service mesh is consistent with the external access protocol configured for the service's Gateway.
-  If the **ERR_UNSAFE_PORT** error is displayed when you use a browser to access the service, that is because the port is identified as a dangerous port by the browser. In this case, you need to use another external port.
