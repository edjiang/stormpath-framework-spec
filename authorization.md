# Authorization

Stormpath's underlying SDKs can retrieve the groups of each user, which can be used to allow users to access different endpoints.

As a convenience to developers using a Stormpath Framework Integration, we allow developers to protect routes by groups, similar to our authenticators. 

**Require Groups**

`requireGroups` is a method that allows a developer to enforce that the user accessing a route is in a specific set of groups, and renders an error if the user is not in the group. 

It first uses the `requireUser` gatekeeper to validate that there is an authenticated user. 

Then, it checks that the user is a member of one of the groups specificed. If not, it renders an error. 

**Errors**

Authorization helpers are terminal and end the request if the user is not authorized, and responds according to content negotiation and produces configuration.

If `application/json` is preferred: Render a `403 Forbidden` with a blank body.

If `text/html` is preferred: Render the unauthorized view. 