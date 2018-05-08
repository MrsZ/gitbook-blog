Fields

[http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html\#issDef](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html#issDef)

* iss: jwt issuer's info
* aud: jwt's recipients, an array of case-sensitive strings
* jti: jwt's id, used to identify the jwt token
* exp
* iat
* sub

Revoke tokens

add jwt's \(aud, jti\) pair into blacklist to avoid replay attack

[https://auth0.com/blog/blacklist-json-web-token-api-keys/](https://auth0.com/blog/blacklist-json-web-token-api-keys/)

Multi-tenancy

Refresh token

[https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/](https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/)

