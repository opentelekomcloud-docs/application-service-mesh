:original_name: asm_faq_0035.html

.. _asm_faq_0035:

Why Cannot I Select the Corresponding Service When Adding a Route?
==================================================================

During adding a route, the target service is filtered based on the corresponding gateway protocol. The filtering rules are as follows:

-  For an HTTP gateway, select an HTTP service.
-  For a TCP gateway, select a TCP service.
-  For a gRPC gateway, select a gRPC service.
-  For an HTTPS gateway, select either an HTTP or a gRPC service.
-  For a TLS gateway which TLS termination is enabled, select a TCP service. If TLS termination for a TLS gateway is disabled, select a TLS service.
