# Authentication

## Overview

All requests to the Tumelo API must be authenticated. Amazon's [AWS Cognito Identity Provider Service](https://aws.amazon.com/cognito/) is the identity provider responsible for issuing the token(s) that you will need to access the Tumelo API itself. You obtain API access tokens by authenticating with Cognito using the credentials issued to your company by Tumelo. You then use the IdToken issued by Cognito in each subsequent request to the Tumelo API. This process is described in detail below.

## Prerequisites

* Install [curl](https://curl.haxx.se/download.html) if you don't already have it installed.
* Install [jq](https://stedolan.github.io/jq/download/) (optional). Instructions for installing `jq` can be found on its [GitHub pages](https://stedolan.github.io/jq/download/). The use of `jq` is optional - it parses and formats the JSON responses, making reading them easier.

## AWS Cognito

Cognito has extensive developer documentation and [resources](https://aws.amazon.com/cognito/dev-resources/) for integrating your  application, including support for Java, PHP, Ruby, .NET, Node.js, Go, iOS, Android, and React Native clients.

For details of how to use the Cognito API itself, please refer to the [Cognito IDP Service](https://docs.aws.amazon.com/cli/latest/reference/cognito-idp/index.html) documentation. The Cognito User Pool Client for the Tumelo API has been configured to support the `USER_PASSWORD_AUTH` flow only.

## Cognito Tokens

Upon successful authentication, Cognito actually issues three different tokens:

    * AccessToken
    * IdToken
    * RefreshToken

The use of each of the tokens is described in detail in the Cognito documentation, however it is the IdToken that is required to access the Tumelo API. The IdToken is an industry-standard [JSON Web Token (JWT)](https://jwt.io) that contains the information necessary for Tumelo to validate the token and provide access to the API. The contents and claims within the JWTs are an implementation detail and are subject to change without notice.

Each IdToken is typically valid for about an hour, after which a new IdToken must be obtained. Using one of Amazon's pre-built libraries makes obtaining a valid IdToken very straightforward, especially since the library caches the tokens and automatically refreshes expired IdTokens as required, without needing to re-authenticate. This greatly minimises the frequency that you need to provide your credentials to obtain a valid IdToken.

While the lifetime of each IdToken is about an hour, the lifetime of the refresh token is typically a month or more. You should ensure your client application handles the case where the Tumelo API returns a `401 Unauthorized` status code as a result of the refresh token having expired. In this situation you should follow the `InitiateAuth` flow again to obtain new Id and refresh tokens.

## Changing your temporary password

You will have been issued with a client ID, a username and a temporary password to gain access to the Tumelo API. The temporary password must be changed the first time you authenticate, to a new strong password of your choosing. Passwords must be 8 characters or more and contain a mixture of upper and lower case letters and digits. You may use non-alphanumeric characters as well, but these are not required.

This section explains the flow for setting your own password using `curl` commands, but for further details and alternative approaches, please consult the AWS Cognito [documentation](https://docs.aws.amazon.com/cli/latest/reference/cognito-idp/index.html).

Once you have changed the password for the first time, you should use the new password you have just set for all subsequent Congito requests.

### Changing your password

1. Create a JSON text file called `temp-auth.json` with the following contents on your local machine, substituting `<YOUR_USERNAME>`,`<TEMP_PASSWORD>` and `<CLIENT_ID>` with the values you have been supplied. This file should __NOT__ be committed to any source control repository, and should only be used for initial experimentation with the Tumelo API.:

```json
{
    "AuthParameters" : {
        "USERNAME" : "<YOUR_USERNAME>",
        "PASSWORD" : "<TEMP_PASSWORD>"
    },
    "AuthFlow" : "USER_PASSWORD_AUTH",
    "ClientId" : "<CLIENT_ID>"
}
```

2. Create a second JSON text file called `challenge-response.json` with the following contents on your local machine, substituting `<YOUR_USERNAME>` and `<CLIENT_ID>` with the values you have been supplied and `<YOUR_NEW_STRONG_PASSWORD>` set to a suitable strong password. This file should __NOT__ be committed to any source control repository, and should only be used for initial experimentation with the Tumelo API. You will obtain the value for the `<SESSION>` placeholder in Step 3 below, but as the values are relatively short-lived it is easier to create this file before making the request to obtain the session token itself:

```json
{
    "ChallengeName": "NEW_PASSWORD_REQUIRED",
    "ChallengeResponses" : {
        "USERNAME" : "<YOUR_USERNAME>",
        "NEW_PASSWORD" : "<YOUR_NEW_STRONG_PASSWORD>"
    },
    "ClientId" : "<CLIENT_ID>",
    "Session" : "<SESSION>"
}
```

3. From the directory in which the `temp-auth.json` file is located, run the following curl command:

```bash
curl -X POST --data @temp-auth.json \
    -H "X-Amz-Target: AWSCognitoIdentityProviderService.InitiateAuth" \
    -H "Content-Type: application/x-amz-json-1.1" \
    https://cognito-idp.eu-west-2.amazonaws.com/ | jq "."
```
If you have not already reset your temporary password, you should see a challenge response similar to the following:

```bash
{
    "ChallengeName": "NEW_PASSWORD_REQUIRED",
    "ChallengeParameters": {
    "USER_ID_FOR_SRP": "<YOUR_USERNAME>",
    "requiredAttributes": "[]",
    "userAttributes": "{\"name\":\"Your Name\",\"phone_number\":\"+447788990011\",\"email\":\"your_email@company.com\"}"
    },
    "Session": "1whYGhuZiDYTgur1_eBfiD7tRJm1F4jtDOSSw6nYgcQsV_Y8SG7U3uY2u-MHO8PP8czoM_Kb9IVVBo6EqxWjte5UJ9IpVRUT8rY-FDFOGdsbgsL5y0qd4lN-_IoHg4uFcXPYmIuCq-pQXkqe1NkQTfkN86za-XeRo-ZODzdp8k4IwaUY5FHehjk-GtRfUx5_up3ePyXLPWwOLoKtR96a7EmaGQ9OeQyLZX0UItiIiWmv9l9W93GwWhr5vyJnmc8nkGLWyoEL-_1poOsuf-pS5rwSrOV9umrjhDbBf0wUR0xR6bVZClrHI8YNQtxn4YD6VKWPO6rQ0rQPHBucl7PAYzsuO9FGGwW53UHJZIBllVf0vlPxyURSoHADYClArSSJUq_UaWosgFhh2TJaqbCRW5-7AOGsmAXWsxdHeTQGn7plt-INSZeEJFRRHq9pAABi19fv0WRQSZaz7PnSkeve-GjCMww55q4DCmRsJ8ODRqsFOYh_6vjj7zjG7befhcog-CpfWPZBdaQM1vcnk5nWmmgnRRSFrqv90EzSvaDpDQEGWhrUZ78xm3ZaWzqVL370HJGcZThD8aQV3NALn_pvxBJJCQMMUzwwSVE_HO064mAL2voiw41vpQa_ope4_u2qQ1XRp079Id8hCNRfJyssJ4Mi7v7VeHn-IppqMs26DGwWn9spVNeOrjQ-yMoX1OapIhfdkOaofjavGGg9m_IwgF0epdxzyrFYRgoh-zC4gCJIzeWZivkRHmcL8V6uPMSvWu7zZ_ING3Xfwik4Nu4OtKuAf7MjAGcD9WoNXV2rhpFXeOlEZ7BWlDFNobvER496GfewUuHzVHtx6BZzaFbejOO5ZBNcQFLWlGAvN1avCUA_81FCyEKbtMunKyzC279QkFcw9vD7TDXTT5FOGsmkp4EkWct0S_Y9zEDKejylsFAjsVCOFwcAIux9RYgrajP2Q32YUA"
}
```

4. Copy the value of the Session attribute (not including the enclosing double quotes) into the `challenge-response.json` file you created earlier, replacing the `<SESSION>` placeholder and save it.

5. From the directory in which the `challenge-response.json` file is located, run the following curl command:

```bash
curl -X POST --data @challenge-response.json \
    -H "X-Amz-Target: AWSCognitoIdentityProviderService.RespondToAuthChallenge" \
    -H "Content-Type: application/x-amz-json-1.1" \
    https://cognito-idp.eu-west-2.amazonaws.com/ | jq "."
```

6. You should see a response similar to that below, indicating that your password has been reset to the one you provided, and that you have been successfully authenticated.

```bash
{
    "AuthenticationResult": {
        "AccessToken": "ACCESS_TOKEN_VALUE",
        "ExpiresIn": 3600,
        "IdToken": "ID_TOKEN_VALUE",
        "TokenType": "Bearer"
    },
    "ChallengeParameters": {}
}
```

### Obtaining an IdToken

Once you have reset your temporary password, subsequent authentication requests do not include the challenge response step. In order to obtain the token(s) that you need to access the Tumelo API itself, you should use your ClientID, username and the password you set above to invoke the Cognito IDP `InitiateAuth` API call. Whilst we strongly recommend the use of one of the official Amazon client libraries for your production application, the following steps can be used to get up and running quickly using a curl request.

1. Create a JSON text file called `tumelo-api-auth.json` with the following contents on your local machine, substituting `<YOUR_USERNAME>` and `<CLIENT_ID>` with the values you have been supplied. You should use the new strong password that you set in the steps above in place of `<YOUR_PASSWORD>`. This file should __NOT__ be committed to any source control repository, and should only be used for initial experimentation with the Tumelo API.:

```
{
    "AuthParameters" : {
        "USERNAME" : "<YOUR_USERNAME>",
        "PASSWORD" : "<YOUR_PASSWORD>"
    },
    "AuthFlow" : "USER_PASSWORD_AUTH",
    "ClientId" : "<CLIENT_ID>"
}
```

2. From the directory in which the `tumelo-api-auth.json` file is located, run the following curl command:

```bash
curl -X POST --data @tumelo-api-auth.json -s \
    -H "X-Amz-Target: AWSCognitoIdentityProviderService.InitiateAuth" \
    -H "Content-Type: application/x-amz-json-1.1" \
    https://cognito-idp.eu-west-2.amazonaws.com/ | jq ".AuthenticationResult.IdToken"
```

Assuming you have entered the correct credentials you will see a response similar to the following:

```bash
"eyJrbWQiOiI5d2xUaGNrbFZENHQ1dmVzTDQyZnJFMXFQdW1PYTJSSTlOK2w4dklUV3NnPSIsImFsZyI6IlJTMjU2In0.eyJzdWIiOiJlM2IyZmE1NS1mN2ZkLTRmZjktYjg3Zi1lMGM1YzY4ZTBiMTQiLCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAuZXUtd2VzdC0yLmFtYXpvbmF3cy5jb21cL2V1LXdlc3QtMl84MncwaWhybkgiLCJjb2duaXRvOnVzZXJuYW1lIjoiV1lDX1NCX1RFU1QiLCJhdWQiOiI0OW5nZmdwODQ2cTA3Z29wMWtyZ2V1Y3IzbyIsImV2ZW50X2lkIjoiYTM0ODA3MjQtYWRlNC00MWJmLWFiNDctZjc4OWVhNGU1MmYyIiwidG9rZW5fdXNlIjoiaWQiLCJhdXRoX3RpbWUiOjE1Nzg5MjI2OTksIm5hbWUiOiJXeWNUdW1lbG8iLCJjdXN0b206YWxsb3dfbGl2ZSI6ImZhbHNlIiwicGhvbmVfbnVtYmVyIjoiKzQ0Nzc4OTkzMDkyMyIsImV4cCI6MTU3ODkyNjI5OSwiaWF0IjoxNTc4OTIyNjk5LCJlbWFpbCI6Ind5Y0B0dW1lbG8uY29tIn0.ISAdYiF_wF2ukZvZ1gO0unhfyW-jsdYHkwyaIVoZdeO6eAmqI3iEKTxoG9LTQhZ2waRRKkKOGrYAEdFzL1CaEXBn8YMWtAJK_3B5-yIQkysdwKujCuErxWjxUnarucS9wtcFw9arNyIu3-da8s_vGvL7hZLoztP3q45mEYAkNOOESP7R_cUMdEVUagMdD_fUt0ybHl4bIadGBYKA-yX_OE61TteFOY-15Gm8cHx5BOX1iUN-uWufjl1keKibwzxWOzRVRUyrgfRkgLdJGIa9wPWyUqBJ9hbt_6JAo9Pb19G2CHknO0xguxm3MgIfSdV0_GDNoNDtCtv637xQk6H_dQ"
```

Your `<IdToken>` is the long string contained within (but not including) the double quotes. Copy this value and use it in the following step. If you're not using `jq`, you will need to copy the token value from the `AuthenticationResult.IdToken` attribute of the response.

3. To use the `<IdToken>`, include it within the `Authorization` header of each HTTP request to the Tumelo API as

```bash
    Authorization: Bearer <IdToken>
```

For example, you can list the available instruments using the following curl request:

```bash
curl -X GET -H "Authorization: Bearer <IdToken>" \
"https://api.prod.tumelo.com/v1/instruments"
```
