# ID Site

ID Site is a hosted login & registration application that simplifies single-sign on (SSO) flows by providing a common place for redirects and cookie storage. If the developer has chosen to use ID Site, they likely have multiple Stormpath Applications that are redirecting the user to ID Site for authentication. When the user authenticates at ID Site, they are returned to the original application (service provider, AKA the SP) with Stormpath Assertion JWT. The application can verify this token and resolve the account that has authenticated.

If the developer needs to use ID Site, they will enable it with `stormpath.web.idSite.enabled`. When this value is true, we should redirect the user to ID site when the following URIs are accessed with a GET request:

* `stormpath.web.login.uri`
* `stormpath.web.logout.uri`
* `stormpath.web.register.uri`
* `stormpath.web.forgot.uri`

In addition, enabling ID Site in the configuration enables an `/idSiteResult` endpoint. 

# `/idSiteResult`

## Request Types

* GET

## Content Type

* Any

## Parameters

`jwtResponse` - a [Stormpath JWT](http://docs.stormpath.com/guides/using-id-site/#handling-the-callback-to-your-application-from-id-site). This should be handled using the underlying SDK's Stormpath Token authenticator. 

## Response

The `jwtResponse` from ID Site can have three states, with the following response logic: 

**REGISTERED**

A new user was created. Follow the standard post-registration logic (like redirecting to the login page or autologin). 

**AUTHENTICATED**

A user logged in. Follow the standard login logic (like setting cookies, and redirecting the user)

**LOGOUT**

A user logged out. Follow the standard logout logic.

## Errors

If not a valid Stormpath JWT, render a `text/html` 401 Unauthorized` error. 