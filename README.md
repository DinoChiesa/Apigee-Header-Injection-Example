## Header Injection

This is a simple Apigee API Proxy that demonstrates how to perform header
injection.

"Header injection" means... the Proxy sets a new header with a value that it
obtains from ... somewhere.

This specific example injects three headers, the value of which are extracted from
the corresponding claims in the JWT ID Token passed on input:
* `injected-header-jti`
* `injected-header-sub`
* `injected-header-email`


## To Use

1. Open a terminal window.

2. Deploy the API Proxy here using the UI or a command-line tool like
   [importAndDeploy](https://github.com/DinoChiesa/apigee-edge-js-examples/blob/main/importAndDeploy.js):
   ```
   ORG=myorg
   ENV=test
   node ./importAndDeploy.js -v -n -o $ORG -e $ENV -d /path-to-this-apiproxy
   ```

3. Obtain a JWT ID from Google Signin, from this page:
   https://dinochiesa.github.io/goog-signin-widget

4. In the terminal window, set the value of the JWT into the shell variable "JWT":
   ```
   JWT=eyJhbGciOiJS....
   ```

5. From the terminal window, invoke the endpoint on this proxy:
   ```
   curl -i https://$ORG-$ENV.apigee.net/header-injection/t1 -H JWT:$JWT
   ```

   You could also use your favorite API client, like Postman, to send this
   request.

   This proxy connects to a service that "echos" the request that it receives.
   In the response, you'll see the three injected headers,
   `injected-header-jti`, `injected-header-sub`, and `injected-header-email`,
   all with values that mnirror those in the JWT ID Token payload.


## Comments and Highlights

Header Injection is a nice general capability. Apigee can set and unset any
headers, with any content, retrieved from tokens, or from external systems.

The key policy in setting headers is [the AssignMessage
policy](https://docs.apigee.com/api-platform/reference/policies/assign-message-policy).

This proxy also uses the [VerifyJWT policy](). That one plays a supporting role
here. It's not necessary for performing header injection, but it's useful to
extract some data from an encoded form, to have something distinct to inject.


## Disclaimer

This example is not an official Google product, nor is it part of an
official Google product.

## License

This material is copyright 2020 Google LLC and is licensed under the [Apache
2.0 License](LICENSE).
