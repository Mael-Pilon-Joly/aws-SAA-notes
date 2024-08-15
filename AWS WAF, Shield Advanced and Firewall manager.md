# WAF
- Web application firewall
- Can monitor web request that end user send to your application and controll access to your content (based on conditions that you specify).

Resources you can protect:
- Cloudfront, API Gateway, ALB, AppSync, Cognito App Runner service, Verified Access instance.

Possible behaviors:
- Allow all the requests except the ontes that you specify
- Block *
- Count request that match your criteria (Count action track)
- Run CAPTCHA or challenges checks against requests that match your criteria

# Shield Advanced
- Protection against DDoS (Distributed denial of service) attacks for AWS ressources at the network and application layers.

# Firewall Manager
- Provides management of protections like WAF and Shield Advanced across accounts and resources, even as new resources are added.
