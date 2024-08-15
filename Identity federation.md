# Identity Federation Overview:

Identity federation allows users with existing identities (from corporate directories or third-party identity providers) to access AWS resources without needing separate AWS credentials.
Instead of creating IAM users for each external user, you can use IAM roles to grant appropriate permissions.

IAM Identity Center:

It’s recommended to use IAM Identity Center (formerly AWS SSO) with identity federation rather than creating individual IAM users. IAM Identity Center manages user access and provides Single Sign-On (SSO) capabilities.

Federating Users with Amazon Cognito:

Amazon Cognito is recommended for mobile and web applications needing access to AWS resources. It provides user authentication, identity management, and secure access.
Supports various identity providers (e.g., Facebook, Google) and features like developer authenticated identities and unauthenticated (guest) access.

Public Identity Service Providers and OpenID Connect (OIDC):

For web or mobile apps, Amazon Cognito handles integration with public identity providers (e.g., Facebook, Google) and supports anonymous sign-ins.
For more advanced scenarios, you can integrate directly with third-party OIDC providers.

Federating Users with SAML 2.0:

If your organization uses a SAML 2.0 identity provider (e.g., Microsoft Active Directory), you can configure trust with AWS. This allows federated SSO to AWS Management Console or API access.
Example: Federate using SAML 2.0 if your company uses Active Directory Federation Services.

Custom Identity Broker Applications:

If your identity store doesn’t support SAML 2.0, you can build a custom identity broker application.
The broker authenticates users against your existing identity system (e.g., LDAP, Active Directory) and requests temporary AWS credentials.
Users receive temporary security credentials (access key ID, secret access key, and session token) to access AWS resources.

# sts 

1. Temporary Security Credentials
Purpose: STS issues temporary security credentials that consist of an access key ID, a secret access key, and a session token. These credentials are used to make authenticated requests to AWS services.

Duration: These credentials are temporary and can be set to expire after a specified duration (from a few minutes to several hours), reducing the risk of long-term credential exposure.

2. Federated Access
Federation Process: When users are authenticated by an external identity provider (such as SAML 2.0, OIDC, or a custom identity provider), STS can issue temporary credentials that allow these users to access AWS resources based on IAM roles.

Role Assumption: Users or applications assume an IAM role that has specific permissions. STS provides temporary credentials for these roles, enabling users to perform actions permitted by the role’s policy.

3. Key STS APIs
AssumeRole: This API allows a user or application to assume an IAM role and obtain temporary security credentials. It’s commonly used in scenarios where users need to access AWS resources with specific permissions granted by the assumed role.

AssumeRoleWithSAML: This API is used when users are authenticated through SAML 2.0. It allows federated users to assume a role based on their SAML assertions and obtain temporary credentials.

AssumeRoleWithWebIdentity: This API is used for federated users authenticated via web identity providers (like Facebook, Google, or any OIDC provider). It allows users to obtain temporary credentials based on their web identity token.

GetFederationToken: This API is used to obtain temporary credentials for federated users who do not assume a specific IAM role but need access to AWS resources.

4. Use Cases
Web and Mobile Apps: Applications that use Amazon Cognito or other identity providers can leverage STS to grant users temporary access to AWS resources without requiring long-term credentials.

Single Sign-On (SSO): When federating with SAML or other identity providers for SSO, STS provides temporary credentials that enable users to access AWS Management Console or API operations.

Cross-Account Access: STS can be used to grant users in one AWS account temporary access to resources in another account, facilitating cross-account access without needing long-term credentials.

5. Security Benefits
Minimized Exposure: Temporary credentials have a limited lifespan, which minimizes the risk associated with credential exposure or compromise.

Granular Permissions: By assuming roles with specific permissions, federated users get only the access they need, adhering to the principle of least privilege.