:original_name: asm_01_0097.html

.. _asm_01_0097:

Authenticating JWT Requests on the Ingress Gateway Using ASM
============================================================

This section describes how to authenticate JWT requests on the ingress gateway using ASM to ensure that users access services through the ingress gateway with a reliable access token.

Preparations
------------

#. A mesh of version 1.15 or 1.18 has been created.
#. The **httpbin** service that passes the diagnosis exists in the mesh. The image is **httpbin**, the port protocol is **HTTP**, and the port number is **80**.
#. An accessible gateway has been created for the **httpbin** service in the mesh.

Creating JWT Authentication
---------------------------

#. .. _asm_01_0097__li116016915174:

   Create a JWK.

   a. .. _asm_01_0097__li10148154317206:

      Visit `JWT tool website <https://jwt.io/>`__, set **Algorithm** to **RS512**, and obtain the public key (PUBLIC KEY).


      .. figure:: /_static/images/en-us_image_0000001476967692.png
         :alt: **Figure 1** Generating a public key

         **Figure 1** Generating a public key

   b. Select **PEM-to-JWK (RSA Only)** in the `JWK to PEM Convertor online <https://8gwifi.org/jwkconvertfunctions.jsp?spm=a2c4g.11186623.0.0.79074d9bGGmlXG&file=jwkconvertfunctions.jsp>`__ tool, enter the public key obtained in the previous step, and click **submit** to convert the public key into a JWK.


      .. figure:: /_static/images/en-us_image_0000001477287480.png
         :alt: **Figure 2** Converting the public key to a JWK

         **Figure 2** Converting the public key to a JWK

      .. code-block::

         {"kty":"RSA","e":"AQAB","kid":"a78641b9-d81e-4241-b35a-71726c3fa053","n":"u1SU1LfVLPHCozMxH2Mo4lgOEePzNm0tRgeLezV6ffAt0gunVTLw7onLRnrq0_IzW7yWR7QkrmBL7jTKEn5u-qKhbwKfBstIs-bMY2Zkp18gnTxKLxoS2tFczGkPLPgizskuemMghRniWaoLcyehkd3qqGElvW_VDL5AaWTg0nLVkjRo9z-40RQzuVaE8AkAFmxZzow3x-VJYKdjykkJ0iT9wCS0DRTXu269V264Vf_3jvredZiKRkgwlL9xNAwxXFg0x_XFw005UWVRIkdgcKWTjpBP2dPwVZ4WWC-9aGVd-Gyn1o0CLelf4rEjGoXbAAEgAqeGUxrcIlbjXfbcmw"}

#. .. _asm_01_0097__li20211184081913:

   Create JWT authentication.

   a. Log in to the ASM console and click the name of the target service mesh to go to its details page.

   b. In the navigation pane, choose **Service Management**. In the upper right corner of the list, select the namespace that your services belong to.

   c. Locate the **httpbin** service and click **Security** in the **Operation** column. In the window that slides out from the right, click **JWT Authentication** and then **Configure now**. In the displayed dialog box, set the following parameters:

      -  **Issuer**: issuer of the JWT. Set this parameter to **test**.
      -  **Audience**: JWT audiences who use the JWT token to access the target service. Set this parameter to **ASM**.
      -  **JWKS**: JWT information. Set this parameter to {"keys": [*JWK created in* *:ref:`1 <asm_01_0097__li116016915174>`*]}. For example, if the JWK created in :ref:`1 <asm_01_0097__li116016915174>` is **{"kty":"RSA","e":"AQAB","kid":"a78641b9-d81e-4241-b35a-71726c3****"}**, the value of **JWKS** is **{"keys": [{"kty":"RSA","e":"AQAB","kid":"a78641b9-d81e-4241-b35a-71726c3****"}]}**.


      .. figure:: /_static/images/en-us_image_0000001528087425.png
         :alt: **Figure 3** Creating JWT authentication

         **Figure 3** Creating JWT authentication

   d. Click **OK**.

Checking Whether JWT Authentication Takes Effect
------------------------------------------------

#. .. _asm_01_0097__li174941250183818:

   Use `JWT tool <https://jwt.io/>`__ to encode the JWT request information into a JWT token.

   Enter the following JWT request information in the **Decoded** area. The automatically converted JWT token is displayed in the **Encode** area.

   -  **HEADER**: Set **alg** to **RS512**, enter **kid** in the JWK created in :ref:`1 <asm_01_0097__li116016915174>`, and set **typ** to **JWT**.
   -  **PAYLOAD**: Set **iss** to **test** and **aud** to **ASM**. Ensure that the values are the same as the issuer and token audience configured in :ref:`2 <asm_01_0097__li20211184081913>`.
   -  **VERIFY SIGNATURE**: The value must be the same as the public key in :ref:`1.a <asm_01_0097__li10148154317206>`.


   .. figure:: /_static/images/en-us_image_0000001527927469.png
      :alt: **Figure 4** Creating a JWT token

      **Figure 4** Creating a JWT token

#. Access the **httpbin** service through the ingress gateway.

   a. Run the following commands to access the service with the JWT token created in :ref:`1 <asm_01_0097__li174941250183818>`:

      **TOKEN**\ =\ *JWT token created by the :ref:`1 <asm_01_0097__li174941250183818>`*.

      **curl -I -H "Authorization: Bearer $TOKEN" http://** {*External access address of the* **httpbin** *service*}/

      Expected outputs:

      .. code-block::

         HTTP/1.1 200 OK
         server: istio-envoy
         date: Wed, 21 Sep 2022 03:11:48 GMT

   b. Run the following command to access the service with an invalid JWT token:

      **curl -I -H "Authorization: Bearer invalidToken" http://** {*External access address of the* **httpbin** *service*}/

      Expected outputs:

      .. code-block::

         HTTP/1.1 401 Unauthorized
         www-authenticate: Bearer realm="http://***.***.***.***:***/", error="invalid_token"
         content-length: 145
         content-type: text/plain
         date: Wed, 21 Sep 2022 03:12:54 GMT
         server: istio-envoy
         x-envoy-upstream-service-time: 19

   c. Modify the JWT authentication created in :ref:`2 <asm_01_0097__li20211184081913>`, leave the **aud** empty (indicating that the service can be accessed by any services), and run the following command to access the service with the JWT token created in :ref:`1 <asm_01_0097__li174941250183818>`:

      **curl -I -H "Authorization: Bearer $TOKEN" http://** {*External access address of the* **httpbin** *service*}/

      Expected outputs:

      .. code-block::

         HTTP/1.1 200 OK
         server: istio-envoy
         date: Wed, 21 Sep 2022 03:20:07 GMT

   d. Run the following command to access the service without the JWT token:

      **curl -I http://** {*External access address of the* **httpbin** *service*}/

      Expected outputs:

      .. code-block::

         HTTP/1.1 403 Forbidden
         content-length: 85
         content-type: text/plain
         date: Wed, 21 Sep 2022 03:29:31 GMT
         server: istio-envoy
         x-envoy-upstream-service-time: 6

   According to the preceding outputs, the request with the correct JWT token can access the service, and the request with an incorrect JWT token or without a JWT token cannot access the service, which indicate that the request identity authentication takes effect.
