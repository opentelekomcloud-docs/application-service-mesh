:original_name: asm_faq_0008.html

.. _asm_faq_0008:

Why Does Not a Grayscale Policy that Based on Request Content Take Effect for Some Services?
============================================================================================

Symptom
-------

A grayscale policy that based on request content does not take effect on some services.

Analysis
--------

A grayscale policy based on request content is valid only for the entry service that is directly accessed.

Solution
--------

If you want a grayscale policy to be applied to all services in an application, the header information of the HTTP request needs to be transferred in the service code.
