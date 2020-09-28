# Authentication

## Overview

All requests to the Tumelo API must be authenticated using an access token. You can use the `authenticate` API endpoint to obtain an access token using the credentials issued to your company by Tumelo. You then use the token in each subsequent request to the Tumelo API.


#### cURL

Getting an ID token.

```shell
ID_TOKEN=$(curl --location -s --request POST 'https://api.prod.tumelo.com/v1/authenticate' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--data-raw '{
        "habitatId": "{HABITAT_ID}",
        "username": "{USERNAME}",
        "password": "{PASSWORD}"
}' | jq -r '.token')
```

## Changing your temporary password

You will have been issued with a client ID, a username and a temporary password to gain access to the Tumelo API. The temporary password should be changed before using the API in production. Passwords must be 8 characters or more and contain a mixture of upper and lower case letters and digits. You may use non-alphanumeric characters as well, but these are not required.

Once you have changed the password, you should use the new password you have just set for all subsequent `authorize` requests.

## Code example

#### cURL

```shell
curl --location -s --request POST 'https://api.prod.tumelo.com/v1/changePassword' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'Authorization: Bearer '$ID_TOKEN \
--data-raw '{
        "newPassword": "{NEW_PASSWORD}"
}'
```

# Authenticating directly with AWS Cognito

For more advanced use cases you may with to authenticate directly with AWS Cognito.

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


To use the `<IdToken>`, include it within the `Authorization` header of each HTTP request to the Tumelo API as

```bash
    Authorization: Bearer <IdToken>
```

For example, you can list the available instruments using the following curl request:

```bash
curl -X GET -H "Authorization: Bearer <IdToken>" \
"https://api.prod.tumelo.com/v1/instruments"
```
