# ID Site

Framework integrations must implement the `web.idSite.enabled` behavior. 

ID Site is used as a replacement for the `/login`, `/logout`, `/forgot`, and `/register` pages, which will redirect to ID Site instead of performing their default behavior. 

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

If not a valid Stormpath JWT, render a `text/html`401 Unauthorized` error. 