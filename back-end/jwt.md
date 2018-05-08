# Basic Knowledge

## Fields

[http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html\#issDef](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html#issDef)

* iss: jwt issuer's info
* aud: jwt's recipients, an array of case-sensitive strings
* jti: jwt's id, used to identify the jwt token
* exp
* iat
* sub

## Revoke tokens

add jwt's \(aud, jti\) pair into blacklist to avoid replay attack

we can blacklist a jti to prevent a token being used more t han X times

[https://auth0.com/blog/blacklist-json-web-token-api-keys/](https://auth0.com/blog/blacklist-json-web-token-api-keys/)

## Multi-tenancy

the secret can vary based on the JWT issuer

## Refresh token

[https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/](https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/)

# Useful library

express-jwt: [https://github.com/auth0/express-jwt](https://github.com/auth0/express-jwt)

* multi-tenancy
* revoked tokens



