---
title: Secpass APIs Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell

search: true

code_clipboard: true

meta:
- name: description
  content: Document for the Secpass APIs
---

# Welcome to Secpass APIs Document!

This APIs document details HTTP request and response for all Secpass APIs.

## Endpoints
Secpass API endpoints are in the form of `https://${instance}/${provider}/${endpoint}`. Value of `$instance` will be provisioned during application onboarding with Secpass, together with application API key (see the [API Authentication](#api-authentication) section). If a sandbox instance is provided, there will be no API key required.

## API Authentication
Secpass API call requires application authentication by API key which will be provisioned during application onboarding. The API 
key is
placed in **Authorization** header:  

`Authorization: Basic ${API_key}`

## Secpass token consumption
### Secpass token from Singpass Login service
```shell
  # Sample Secpass token
  eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJ1PWE5ODY1ODM3LTdiZDctNDZhYy1iZWY0LTQyYTc2YTk0NjQyNCJ9.E5_qq6PBTIETXA3mPyVpbwoNC-SSrmHoravbG-iSIV4fcmN_dVVbTlvShQVTIWoeACOrtppAvqVqpJBkEnCeXGa3UnomHlpS8xvd3tWl-NT12BYMYgYkNkOT91Auzvmbd4e9rCCW8mYlj8S4YML25S_dJJTQ3NSATRHYH41vXTj-6G8Ko3V4yt5DGRcRa6qARTj1lNZLRXuDNbI9sxQY-zipnSdpSHhsh97wNuFUTIeDu1EjF1_Th9sB676PQgzKxBtpF_hKvT6LzrNZMhyV5Pg7H_BcIMz8VnAxtKgOfv-O0NeqTIMSrinA7NB6YkGVXZw92EnV4jEmy-JUwqnUoA
```
Secpass token is a token that is in the form of compact serialized JWS.

  - <a href='https://www.rfc-editor.org/rfc/rfc7515'>JWS specification</a>

After receiving Secpass token, the application needs to verify the resulting token signature (using Secpass's public certificate). User's information from the payload of that JWS token contains only the UUID value of its Singpass credential.

<aside class="warning">
  On the event of invalid token signature, due to security reason, the application is advised to discard
  the token.
</aside>


> Sample payload of JWS:

```json
{
  "sub": "u=a9865837-7bd7-46ac-bef4-42a76a946424"
}
```

### Secpass token from Singpass Myinfo service

```shell
  # Sample Secpass token
  eyJlcGsiOnsia3R5IjoiRUMiLCJjcnYiOiJQLTI1NiIsIngiOiJBUnZHNEY4Tl8ydFhnVUUtM3pSWEtfa3hVZFY4QTVyX0FVNUxhR3hhdVVBIiwieSI6IjBwZDF5b1FQVXdNeHFkU2sydDBFT0FxOFpUanZrci1sUFZnb2dvTW9EUVkifSwiZW5jIjoiQTI1NkdDTSIsImFsZyI6IkVDREgtRVMifQ..bQ-uu0olNykhxjRI.IndhhSzUTwx6oswbqN1rIQMVc0SSH-Vy3sMuMgxF8bhyc7mhKSpw2M8_luGq9MCpk9cuML8BiwEq5B2WGOoVQzeFyC4lDpc61jZG01nwxc85zkzgTR_znhWBhaTsGLKHpEbm7woWe1aD9fJea8Fd-Fus-w8K1I2vGnTjT6gnsRdaQwWDlSXXYqpBPI7fv7hE4R5PmVilaKBYS6b65aOR3C_VNGaHBowgv3eR45BLv8KTnhqN94_6j0xZrTMwitnQATjoa7I3baxbGX0yIj7JWKz9kvHe6yPB1CZEFhr-jpktdeJf0XtAQ5Xzdl9-C5tWu0cp5EadMC2QCaCe7uQlmu36DmytOtSgNwUdEqRQfdbiVNnoEcvsFomN-JRy9Byg_mhzVDAYdVsdw867Lyb-j0iKHv_avXWE5uG5S-j4r8FZOH2EFOm6hwLcDuffj3H3jARQ8oUz1sUPIHCYlovdRcMAhqN57nFh8j7jCKVHZvAlTFX3Bu0oUpR5nUAaEPkkWck_y2yJ_YT52E-ovEUI5Ps0iMzN6MajVTYVfvBkBtvNvB1QVR0eormIERqtgP5__ujkqiNstJyig2ScRee6f8FcPi8pAfoOQ2SYpR_KVHeyZZRhn_Xmctbp3TX_nl0T2CynMfWCmU6RgCjRVrl2cd67lN57dp6T5j-Cr3Px3DBMjuuqJZ_d0rv33vrpHB4is_p735hXTXAkjlythb6fOHIQbO5gxqiKAWOeKRRvaYA2DOTPEJ90B7ZSIUKCSj2FTfQqP9mq-xoHFl5SAoKdCx0s58Aro8q8w3_hYVLDZzFJMv0ecMawz-3LiTT6ryuCNPvA_mDdaOCajGDRRL5JqrlUVJVEYmiVkj8eAJlL81t1noDfLYGiYug8SI6VPTWc0nxdilJ7ZaKwJzGFI-r2ZZ2Br9L0_1RMCozgukORMiO8YB73wxVtfUmp-Qbup45_tpHDaPtJP__epMP4137KkXNJNZKyOc44mZemlswVlZXTkP48uxtT-w.kICyvx1u00C3y9R9KPhl4A
```

Secpass token is a token that is in the form of compact serialized JWE whose payload after being decrypted is a compact serialized
JWS.  

  - <a href='https://www.rfc-editor.org/rfc/rfc7516'>JWE specification</a>  
  - <a href='https://www.rfc-editor.org/rfc/rfc7515'>JWS specification</a>

### Howto get the payload
After receiving Secpass token, the application first needs to decrypt the token (using application's private key) to extract the 
payload, then needs to verify the resulting token signature (using Secpass's public certificate). User's information is in the 
payload of that JWS token. Secpass does not modify the 
JSON data structure and leaves it fully intact as received from **Myinfo**/**Myinfo Business**. Consult 
**Myinfo**/**Myinfo Business** APIs documents to traverse the data effectively.

<aside class="warning">
  On the event of invalid token signature, due to security reason, the application is advised to discard
  the token.
</aside>

```shell
  # Sample payload of decrypted Secpass token
  eyJhbGciOiJFUzI1NiJ9.eyJuYW1lIjp7Imxhc3R1cGRhdGVkIjoiMjAyMy0wMy0wMiIsInNvdXJjZSI6IjEiLCJjbGFzc2lmaWNhdGlvbiI6IkMiLCJ2YWx1ZSI6IkJIQVNLQVIgTklMQU0gR0FESEFWSSJ9LCJkb2IiOnsibGFzdHVwZGF0ZWQiOiIyMDIzLTAzLTAyIiwic291cmNlIjoiMSIsImNsYXNzaWZpY2F0aW9uIjoiQyIsInZhbHVlIjoiMTk5MS0xMi0wNCJ9LCJ1aW5maW4iOnsibGFzdHVwZGF0ZWQiOiIyMDIzLTAzLTAyIiwic291cmNlIjoiMSIsImNsYXNzaWZpY2F0aW9uIjoiQyIsInZhbHVlIjoiUzkxNTM2MTZBIn0sIm5hdGlvbmFsaXR5Ijp7Imxhc3R1cGRhdGVkIjoiMjAyMy0wMy0wMiIsImNvZGUiOiJTRyIsInNvdXJjZSI6IjEiLCJjbGFzc2lmaWNhdGlvbiI6IkMiLCJkZXNjIjoiU0lOR0FQT1JFIENJVElaRU4ifSwibWFycmllZG5hbWUiOnsibGFzdHVwZGF0ZWQiOiIyMDIzLTAzLTAyIiwic291cmNlIjoiMSIsImNsYXNzaWZpY2F0aW9uIjoiQyIsInZhbHVlIjoiIn19.h2DCBNdj5Zy6hLe4PfZJW0umD9Eb9B3BQcQ8xm35Q97oniijFI_4yeHsG_qMDVcqmlUe1U6LTq5rw2ZrOt0SUg
```

> Sample payload of JWS:

```json
  {
    "name": {
      "lastupdated": "2023-03-02",
      "source": "1",
      "classification": "C",
      "value": "BHASKAR NILAM GADHAVI"
    },
    "dob": {
      "lastupdated": "2023-03-02",
      "source": "1",
      "classification": "C",
      "value": "1991-12-04"
    },
    "uinfin": {
      "lastupdated": "2023-03-02",
      "source": "1",
      "classification": "C",
      "value": "S9153616A"
    },
    "nationality": {
      "lastupdated": "2023-03-02",
      "code": "SG",
      "source": "1",
      "classification": "C",
      "desc": "SINGAPORE CITIZEN"
    },
    "marriedname": {
      "lastupdated": "2023-03-02",
      "source": "1",
      "classification": "C",
      "value": ""
    }
  }
```  

| Secpass token metadata                | Value                                                                                               |
|---------------------------------------|-----------------------------------------------------------------------------------------------------|
| JWE **enc**                           | *A256GCM*                                                                                           |
| JWE **alg**                           | *ECDH-ES* (<a href='https://www.rfc-editor.org/rfc/rfc7518#page-16'>specification</a>)              |
| JWE decryption key for CEK encryption | Application *EC* private key whose public key was provided to Secpass during application onboarding |
| JWS **alg**                           | *ES256*                                                                                             |
| JWS signature verification key        | Secpass public key which was provided to application by Secpass during application onboarding       |


# Singpass Login Integration
## Authorisation Request API
### Description
This API returns a Singpass login URL. The user-agent/browser should redirect user to this URL when user trigger login with Singpass.
### HTTP Request
`POST https://${instance}/oidc/singpass/authReqUri`

```shell
curl --location 'https://${instance}:4201/oidc/singpass/authReqUri' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ${API_key}' \
--data '{ "purpose": "login" }'
```

| Request body | Description                                                                                      |
|-----------------|--------------------------------------------------------------------------------------------------|
| *purpose*          | Can take the value *login* |

### HTTP Response
<aside class="success">
This endpoint returns a Singpass login URL in the response body. The user-agent/browser should redirect user to this URL when user trigger login with Singpass.
</aside>

> Sample successful response

```json
{
    "authReqUri": "http://adnsg-public.southeastasia.cloudapp.azure.com:5157/singpass/authorize?purpose=login&scope=openid&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%3A4200&state=tMrpao0g_V2paGvT4fEC57oGC9xFW7FpuQOTuStY2Qg&nonce=DH2HjZJIbsBpmuppBj_vIWzLMWmpaA0b-kKP9AO--68&client_id=f3fdfa0cae866ba3b81777c5bfc44206"
}
```

| HTTP Response Status | Meaning                                                    |
|-----|-----------------------------------------------------------------------------|
| 200 | Redirect -- Proceed to redirect your user to the URI in the response body.  |
| 403 | Forbidden -- Invalid API key.                                               |
| 500 | Internal Server Error -- We had a problem with our server. Try again later. |

## User Info API
### Description
This API is to exchange a *code* and *state* which are in the request URI that **Singpass** redirects the user to the application's callback URL after their successful authentication, to get the Secpass token.
### HTTP Request
`POST https://${instance}/oidc/singpass/userInfo`

```shell
curl --location 'https://${instance}:4201/oidc/singpass/userInfo' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ${API_key}' \
--data '{ "authCode": "XXXXX", "state": "XXXXX" }
```
| Request body | Description                                                                                      |
|-----------------|--------------------------------------------------------------------------------------------------|
| *authCode*       | a code received as request's query string at the application's callback URL after successful authentication at Singpass Login portal |
| *state*          | a state value received as request's query string at the application's callback URL after successful authentication at Singpass Login portal" |

### HTTP Response
On successful response i.e. status code 200, the response body is a [Secpass token from Singpass Login service](#secpass-token-from-singpass-login-service). The response *Content-Type* is `application/jose`.

> Sample successful response

```json
{
    "token": "eyJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJ1PWE5ODY1ODM3LTdiZDctNDZhYy1iZWY0LTQyYTc2YTk0NjQyNCJ9.E5_qq6PBTIETXA3mPyVpbwoNC-SSrmHoravbG-iSIV4fcmN_dVVbTlvShQVTIWoeACOrtppAvqVqpJBkEnCeXGa3UnomHlpS8xvd3tWl-NT12BYMYgYkNkOT91Auzvmbd4e9rCCW8mYlj8S4YML25S_dJJTQ3NSATRHYH41vXTj-6G8Ko3V4yt5DGRcRa6qARTj1lNZLRXuDNbI9sxQY-zipnSdpSHhsh97wNuFUTIeDu1EjF1_Th9sB676PQgzKxBtpF_hKvT6LzrNZMhyV5Pg7H_BcIMz8VnAxtKgOfv-O0NeqTIMSrinA7NB6YkGVXZw92EnV4jEmy-JUwqnUoA"
}
```

| HTTP Response Status | Meaning                                                     |
|-----|------------------------------------------------------------------------------|
| 200 | Successfull -- Return encrypted JWS Secpass token.                           |
| 400 | Bad request -- Invalid *state* value.                                        |
| 403 | Forbidden -- Invalid API key.                                                |
| 500 | Internal Server Error -- We had a problem with our server. Try again later.  |


# Myinfo Integration
## Authorisation Request API
### Description
This API is to get an *OAuth authorisation request*, which can be used for sending request to **Myinfo** */authorise* API.
### HTTP Request
`GET https://${instance}/myinfo/init`

```shell
  curl -X GET -H 'Authorization: Basic ${API_key}' 'https://${instance}/myinfo/init'
```
### HTTP Response
<aside class="success">
This endpoint returns no response body. A successful call is indicated by the event that application receives a 302 response
with redirect URI in the Location Header.
</aside>

| HTTP Response Status | Meaning                                                    |
|-----|-----------------------------------------------------------------------------|
| 302 | Redirect -- Proceed to redirect your user to the URI in Location Header.    |
| 403 | Forbidden -- Invalid API key.                                               |
| 500 | Internal Server Error -- We had a problem with our server. Try again later. |

## Token API
### Description
This API is to exchange a *code* and *state* which are in the request URI that **Myinfo** redirects the user to after
their authentication and consent giving, to get the Secpass token.
### HTTP Request
`GET https://${instance}/myinfo/token?code=${code}&state=${state}`

```shell
  curl -X GET -H 'Authorization: Basic ${API_key}' 'https://${instance}/myinfo/token?code=${code}&state=${state}'
```

| Query Parameter | Description                                                                                      |
|-----------------|--------------------------------------------------------------------------------------------------|
| *code*          | Authorization code ${code} is received from **Myinfo** after user authenticates and gives their consent. |
| *state*         | This ${state} is received from **Myinfo** after user authenticates and gives their consent. |

### HTTP Response
On successful response i.e. status code 200, the response body is a [Secpass token from Singpass Myinfo service](#secpass-token-from-singpass-myinfo-service). The response 
*Content-Type* is `application/jose`. Follow the [instruction](#howto-get-the-payload) to decrypt and verify Secpass token to get the JSON string for your application usage.

> Sample successful response

```shell
  eyJlcGsiOnsia3R5IjoiRUMiLCJjcnYiOiJQLTI1NiIsIngiOiJBUnZHNEY4Tl8ydFhnVUUtM3pSWEtfa3hVZFY4QTVyX0FVNUxhR3hhdVVBIiwieSI6IjBwZDF5b1FQVXdNeHFkU2sydDBFT0FxOFpUanZrci1sUFZnb2dvTW9EUVkifSwiZW5jIjoiQTI1NkdDTSIsImFsZyI6IkVDREgtRVMifQ..bQ-uu0olNykhxjRI.IndhhSzUTwx6oswbqN1rIQMVc0SSH-Vy3sMuMgxF8bhyc7mhKSpw2M8_luGq9MCpk9cuML8BiwEq5B2WGOoVQzeFyC4lDpc61jZG01nwxc85zkzgTR_znhWBhaTsGLKHpEbm7woWe1aD9fJea8Fd-Fus-w8K1I2vGnTjT6gnsRdaQwWDlSXXYqpBPI7fv7hE4R5PmVilaKBYS6b65aOR3C_VNGaHBowgv3eR45BLv8KTnhqN94_6j0xZrTMwitnQATjoa7I3baxbGX0yIj7JWKz9kvHe6yPB1CZEFhr-jpktdeJf0XtAQ5Xzdl9-C5tWu0cp5EadMC2QCaCe7uQlmu36DmytOtSgNwUdEqRQfdbiVNnoEcvsFomN-JRy9Byg_mhzVDAYdVsdw867Lyb-j0iKHv_avXWE5uG5S-j4r8FZOH2EFOm6hwLcDuffj3H3jARQ8oUz1sUPIHCYlovdRcMAhqN57nFh8j7jCKVHZvAlTFX3Bu0oUpR5nUAaEPkkWck_y2yJ_YT52E-ovEUI5Ps0iMzN6MajVTYVfvBkBtvNvB1QVR0eormIERqtgP5__ujkqiNstJyig2ScRee6f8FcPi8pAfoOQ2SYpR_KVHeyZZRhn_Xmctbp3TX_nl0T2CynMfWCmU6RgCjRVrl2cd67lN57dp6T5j-Cr3Px3DBMjuuqJZ_d0rv33vrpHB4is_p735hXTXAkjlythb6fOHIQbO5gxqiKAWOeKRRvaYA2DOTPEJ90B7ZSIUKCSj2FTfQqP9mq-xoHFl5SAoKdCx0s58Aro8q8w3_hYVLDZzFJMv0ecMawz-3LiTT6ryuCNPvA_mDdaOCajGDRRL5JqrlUVJVEYmiVkj8eAJlL81t1noDfLYGiYug8SI6VPTWc0nxdilJ7ZaKwJzGFI-r2ZZ2Br9L0_1RMCozgukORMiO8YB73wxVtfUmp-Qbup45_tpHDaPtJP__epMP4137KkXNJNZKyOc44mZemlswVlZXTkP48uxtT-w.kICyvx1u00C3y9R9KPhl4A
```

| HTTP Response Status | Meaning                                                     |
|-----|------------------------------------------------------------------------------|
| 200 | Successfull -- Return encrypted JWS Secpass token.                           |
| 400 | Bad request -- Invalid *state* value.                                        |
| 403 | Forbidden -- Invalid API key.                                                |
| 404 | Not found - Invalid **Myinfo** server response.                              |
| 500 | Internal Server Error -- We had a problem with our server. Try again later.  |

# Myinfo Business Integration
## Authorisation Request API
### Description
This API is to get an *OAuth authorisation request*, which can be used for request to **Myinfo Business** */authorise* API.
### HTTP Request
`GET https://${instance}/myinfobiz/init`

```shell
  curl -X GET -H 'Authorization: Basic ${API_key}' 'https://${instance}/myinfobiz/init'
```
### HTTP Response
<aside class="success">
This endpoint returns no response body. A successful call is indicated by the event that application receives a 302 response
with redirect URI in the Location Header.
</aside>

| HTTP Response Status | Meaning                                                    |
|-----|-----------------------------------------------------------------------------|
| 302 | Redirect -- Proceed to redirect your user to the URI in Location Header.    |
| 403 | Forbidden -- Invalid API key.                                               |
| 500 | Internal Server Error -- We had a problem with our server. Try again later. |

## Token API
### Description
This API is to exchange a *code* and *state* which are in the request URI that **Myinfo business** redirects the user to after
their authentication and consent giving, to get the Secpass token.
### HTTP Request
`GET https://${instance}/myinfobiz/token?code=${code}&state=${state}`

```shell
  curl -X GET -H 'Authorization: Basic ${API_key}' 'https://${instance}/myinfobiz/token?code=${code}&state=${state}'
```

| Query Parameter | Description                                                                                               |
|-----------------|-----------------------------------------------------------------------------------------------------------|
| *code*          | Authorization code ${code} is received from **Myinfo business** after user authenticates and gives their consent. |
| *state*         | This ${state} is received from **Myinfo business** after user authenticates and gives their consent. |

### HTTP Response
On successful response i.e. status code 200, the response body is a [Secpass token from Singpass Myinfo service](#secpass-token-from-singpass-myinfo-service). The response 
*Content-Type* is `application/jose`. Follow the [instruction](#howto-get-the-payload) to 
decrypt and verify Secpass token to get the JSON string for your application usage.

> Sample successful response

```shell
  eyJlcGsiOnsia3R5IjoiRUMiLCJjcnYiOiJQLTI1NiIsIngiOiJBUnZHNEY4Tl8ydFhnVUUtM3pSWEtfa3hVZFY4QTVyX0FVNUxhR3hhdVVBIiwieSI6IjBwZDF5b1FQVXdNeHFkU2sydDBFT0FxOFpUanZrci1sUFZnb2dvTW9EUVkifSwiZW5jIjoiQTI1NkdDTSIsImFsZyI6IkVDREgtRVMifQ..bQ-uu0olNykhxjRI.IndhhSzUTwx6oswbqN1rIQMVc0SSH-Vy3sMuMgxF8bhyc7mhKSpw2M8_luGq9MCpk9cuML8BiwEq5B2WGOoVQzeFyC4lDpc61jZG01nwxc85zkzgTR_znhWBhaTsGLKHpEbm7woWe1aD9fJea8Fd-Fus-w8K1I2vGnTjT6gnsRdaQwWDlSXXYqpBPI7fv7hE4R5PmVilaKBYS6b65aOR3C_VNGaHBowgv3eR45BLv8KTnhqN94_6j0xZrTMwitnQATjoa7I3baxbGX0yIj7JWKz9kvHe6yPB1CZEFhr-jpktdeJf0XtAQ5Xzdl9-C5tWu0cp5EadMC2QCaCe7uQlmu36DmytOtSgNwUdEqRQfdbiVNnoEcvsFomN-JRy9Byg_mhzVDAYdVsdw867Lyb-j0iKHv_avXWE5uG5S-j4r8FZOH2EFOm6hwLcDuffj3H3jARQ8oUz1sUPIHCYlovdRcMAhqN57nFh8j7jCKVHZvAlTFX3Bu0oUpR5nUAaEPkkWck_y2yJ_YT52E-ovEUI5Ps0iMzN6MajVTYVfvBkBtvNvB1QVR0eormIERqtgP5__ujkqiNstJyig2ScRee6f8FcPi8pAfoOQ2SYpR_KVHeyZZRhn_Xmctbp3TX_nl0T2CynMfWCmU6RgCjRVrl2cd67lN57dp6T5j-Cr3Px3DBMjuuqJZ_d0rv33vrpHB4is_p735hXTXAkjlythb6fOHIQbO5gxqiKAWOeKRRvaYA2DOTPEJ90B7ZSIUKCSj2FTfQqP9mq-xoHFl5SAoKdCx0s58Aro8q8w3_hYVLDZzFJMv0ecMawz-3LiTT6ryuCNPvA_mDdaOCajGDRRL5JqrlUVJVEYmiVkj8eAJlL81t1noDfLYGiYug8SI6VPTWc0nxdilJ7ZaKwJzGFI-r2ZZ2Br9L0_1RMCozgukORMiO8YB73wxVtfUmp-Qbup45_tpHDaPtJP__epMP4137KkXNJNZKyOc44mZemlswVlZXTkP48uxtT-w.kICyvx1u00C3y9R9KPhl4A
```

| HTTP Response Status | Meaning                                                                      |
|----------------------|------------------------------------------------------------------------------|
| 200                  | Successfull -- Return encrypted JWS Secpass token.                           |
| 400                  | Bad request -- Invalid *state* value.                                        |
| 403                  | Forbidden -- Invalid API key.                                                |
| 404                  | Not found -- Invalid **Myinfo Business** server response.                    |
| 500                  | Internal Server Error -- We had a problem with our server. Try again later.  |
