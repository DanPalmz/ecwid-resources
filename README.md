# Ecwid Resources

## Disclaimer
I am just a hobbiest developer who's been using the [Ecwid](https://www.ecwid.com) E-commerce Shopping Cart for work and developing some coding skills.   I've made a public Python API wrapper [pyecwid](https://pypi.org/project/pyecwid/) and will probably release a TypeScript one soon.   

I have no assoication with Ecwid so use these resources with care!

## Postman Collection - Reformatted
### Why?
The Postman collection available from https://api-playground.ecwid.com/#!/ is exported in a Postman v1 format which won't import directly into modern Postman versions.  I've updated the collection to v2 using:
```console
$ npm install -g postman-collection-transformer
$ postman-collection-transformer convert -i ./ecwid_postman_collection.json -o ./ecwid_reformatted_postman_collection.json -j 1.0.0 -p 2.0.0 -P
```

I've then tidied up the URLs for each endpoint/query by:
* using variables for the ECWID_API_HOST and ECWID_STORE_ID
* removing the token paramater from individual URLS.   This is instead in an AUTH section for the entire collection.

This enables you to quickly switch between different environments (Test store, live store, even different hostnames for testing.)
![Environment Image](./postman/postman_environment.png?raw=true)

### How to use
* Import the collection into Postman
* Set variables for:
    * ECWID_STORE_ID
    * ECWID_TOKEN_SECRET
    * ECWID_API_HOST (app.ecwid.com)
* If required token settings may be modified for the entire collection by updating the variable or changing values in Collection -> Authorization.<br />
![Authorization Image](./postman/postman_authorization.png?raw=true)

### Sample Usage
Note: the token is not able to be modified in the query window - but it also isn't in the URL at the top anymore!<br />
![Sample Image](./postman/postman_sample.png?raw=true)

## Documentation: Postman OAuth 2.0 token request settings.
Details from https://my.ecwid.com/cp/#develop-apps you require:
* Under App Keys within custom app:
    * Client ID
    * Client Secret (*Note: different from "Secret Token"*)
* Callback URL: *Value you requested to be set by support*

* Type: OAuth 2.0
* Grant Type: Authorization Code
* Callback URL
* Auth URL: https://my.ecwid.com/api/oauth/authorize
* Access Token URL: https://my.ecwid.com/api/oauth/token
* Client ID
* Client Secret
* Scope: *list of access scopes - your Custom App shows those authorised for use - change from commas to spaces*

### Notes:
Doesn't require the Callback URL to be active - you just need to know it.

![Sample Image](./postman/postman_oauth2.png?raw=true)
