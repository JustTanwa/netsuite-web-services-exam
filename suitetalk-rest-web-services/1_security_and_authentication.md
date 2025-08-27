# Security Techniques and Authentication Configuration

- Always use dedicated roles with REST Web Services to control fine-grained minimal required permissions
- Use Web Services Only Role to prvent UI access and horizontal role movement in the UI. If the user has multiple roles, user can log in UI as SOAP WS role and move to another.
- Use OAuth 2.0 for authentication when possible
- Check out how to set up integration record and generate access tokens
- Token Key and Secret are unique to each account (must be regenerated after sandbox refresh, does not affect production env)
- Consumer key and secret can be shared between accounts, so don't regenerate after sandbox refresh if used in production. 
- SuiteAnalytics Workbook is required to access the SuiteQL endpoint of REST
- REST Web Services and Log in using Access Token is requirement permissions on the role

## Integration record configuration

This record allow you to manage and maintain the REST Web Services requests.

- View REST WS Requests Logs
- Manage concurrency limit for the integration
- Block access to the integration
- Select authentication method (TBA or OAuth 2.0 Flows) and additionally select the scope for Restlet, REST and SuiteAnalytics Connect.
- Can be bundled and shared (Recommended to create individual for sandbox and production to avoid issues)


## OAuth 2.0

With REST Web Services integration can use the OAuth 2.0 standard which increases thge overall security that is following the industry standards.

The integration make use of access token and avoid the need to store user credentials. REST does not support login through user credential in any case.

- OAuth 2.0 Feature requires enabling
- Integration Role requires OAuth 2.0 permissions (Log in using OAuth 2.0 Access Token)
- OAuth 2.0 Authorized Applications Management permission give control to view and revoke authorized applications and set up client credential flows

**Recommended to use OAuth 2.0 over TBA when possible**

### OAuth 2.0 (authorization code grant)

Authorization Code Grant flow is a redirect-based authorication code which require the user to login and authorize the application, upon authorization the access code is redirected to the URI set up in the integration record for the integration to use.

[Full Details Of the Flow](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html)

1. Get Request to Authorization Endpoint (A user interaction is required to provide authorization to the application via the consent form)
2. Application use the code from Step 1 to set POST request to token endpoint for an access token and refresh token.
3. Application can now use access token to interact with REST Web Services and refresh when needed with the refresh token

### OAuth 2.0 (client credentials)

This method is sometimes refer to Machine-to-Machine flow where a user interaction is not required. An administrator, or a user assigned a role with the OAuth 2.0 Authorized Applications Management permission, can create or revoke a mapping for the OAuth 2.0 client credentials flow.

Creating a new OAuth 2.0 Client Credentials (M2M) require you to generate a private/public key pair where you would upload the public certifcate into Netsuite. You can generate this using openSSL. The private key part is used to sign a JSON Web Token (JWT) which is sent via POST request to the token endpoint for an access token.

[Full Details of M2M Setup](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_162686838198.html)
[JWT Structure](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_162790605110.html)

**NOTE:** Applications authorized using the OAuth 2.0 feature in your NetSuite production account aren't copied to your Release Preview or to your sandbox accounts. Users must authorize applications explicitly in Release Preview or in a sandbox to test OAuth 2.0 feature in these accounts. Each time the sandbox is refreshed, users must authorize applications explicitly in the sandbox.
