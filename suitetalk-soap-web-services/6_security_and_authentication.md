# Security Techniques and Authentication Configuration

- Always use dedicated roles with SOAP WS to control fine-grained minimal required permissions
- Use Web Services Only Role to prvent UI access and horizontal role movement in the UI. If the user has multiple roles, user can log in UI as SOAP WS role and move to another.
- Use Token Based Authentication, with new SOAP WS endpoint (2020_1 and up) username and password is no longer supported. 
- Check out how to set up integration record and generate access tokens
- Request must be sent using TLS (https)
- With TBA, including application ID causes request to fail.
- Token Key and Secret are unique to each account (must be regenerated after sandbox refresh, does not affect production env)
- Consumer key and secret can be shared between accounts, so don't regenerate after sandbox refresh if used in production. 

## Integration record configuration

This record allow you to manage and maintain the SOAP Web Services requests.

- View SOAP WS Requests Logs
- Manage concurrency limit for the integration
- Block access to the integration
- Select authentication method
- Can be bundled and shared (Recommended to create individual for sandbox and production to avoid issues)

