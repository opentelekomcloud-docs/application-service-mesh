:original_name: asm_faq_0007.html

.. _asm_faq_0007:

Why Can't I Change the Image Used for the Grayscale Version When Performing a Grayscale Release?
================================================================================================

Symptom
-------

When I perform a grayscale release, the image used for the grayscale version cannot be changed.

Analysis
--------

When performing the grayscale release on a service, you can only change the tags of the image used by the service.

Solution
--------

Pack the required image into a different tag of the same image and push it to the image repository. Then, select the newly pushed image tag when you perform a grayscale release on the service.
