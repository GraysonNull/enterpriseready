+++
date = "2016-10-25T00:00:00Z"
title = "Product Security"
featureslug = "product-security"
type = "feature"
hero = "/images/product-security.svg"
+++

Security isn't a topic to discuss by itself, it should be part of the conversation around everything discussed on EnterpriseReady. For SaaS companies working with larger enterprise IT buyers it is incredibly important for this to be an area of strength. Most enterprises will provide potential software vendors with long third-party [vendor security questionnaires](https://www.vendorsecurityalliance.org/questions). These documents generally cover a broad range of security topics including product security, physical office security, employee screening, office network security, business continuity, upstream vendor security, disaster recovery, data security, secure IT policy, asset security and data center security in order to evaluate the overall security posture of an organization.

For the purpose of this guide we’re going to focus on product related security issues. These be broken into 3 primary categories of development: security, ops security and product security. We also recommend a detailed review of the [security controls recommended by OWASP](https://www.owasp.org/index.php/Category:Control).

## Ops
----  
**Communication security**  
TLS all the things (including internal server-to-server communication). It's just not acceptable to use unencrypted communication inside your datacenter.

**Automation**  
Reproducibility is key to ensuring consistent and intended environments by removing opportunity for human error. Without scripted and reproducible deployments, you will end up with a collection of unaudited, artisanally configured servers that could have undetected security vulnerabilities on them.

**Automatically Block Attacks**  
There are some external products and services that can help detect when your network has been compromised and even automatically block access to bad actors. Some examples of products to evaluate are: [SignalSciences](https://www.signalsciences.com), [Tenable](https://www.tenable.com), [AlienVault](https://www.alienvault.com) or [Snort](https://www.snort.org).

**API Rate Limiting**
Without rate limiting, your API is subject to brute force attacks. Consider enforcing rate limits in an upstream load balancer. It's also recommended that unauthenticated requests have a considerably lower rate limit than authenticated requests.

**DDOS prevention**  
If you've prevented rogue traffic from accessing your servers and network, it's still possible for external services to block anyone else from using your service by creating a distributed, denial-of-service attack. To prevent this, it's recommended to use a 3rd party service such as [Cloudflare](https://www.cloudflare.com) or [Akamai](https://www.akamai.com) who have experience managing DDOS attacks.

**Network Access Control**  
Create private networks by leveraging cloud hosting features such as VPCs and VPN connections when possible. Don't treat your office location as an extension of this network. Anyone who needs to access the production network should have a VPN connection from their own device.

**Public Footprint**  
Servers should not have public IP addresses unless absolutely needed. All unnecessary ports should be blocked. Only allow SSH connections from internal (VPN) connections. Moving the SSH port to a different port isn't a secure solution.

**Data security**  
Encryption, least privilege, deletion, auditing use of privileges. When possible (which should be all of the time), leverage systems to encrypt data while at rest. Store PII (Personally Identifiable Information) in separate systems. Be aware of any compliance and regulatory processes that are specific to your industry and be prepared to explain how you follow them.

**Separation of roles**  
Most large enterprises will require that you have different roles for development, ops, monitoring, etc. It's important to be able to provide this, but there isn't a requirement that a single person cannot be in multiple roles. It should be structured so that a developer who also has SSH access to production servers cannot be assuming both roles simultaneously though.

**Leverage trusted images**  
If using Docker, enable Content Trust to ensure the image lifecycle is securely managed

**Monitoring**  
All of the best security measures in place aren't enough if you don't have monitoring in place to know when you've been compromised. Invest in detailed monitoring that will alert you when unexpected events occur such as SSH connections from new IP addresses, high network throughput, high CPU, new processes running on servers, etc.

**Enable and Enforce Two Factor Auth**  
For any system that support two-factor authentication, you should require that your own employees and contractors enable this feature. Many product even have a way to enforce it for all members of your team.  

## Development
----  
**Code reviews**  
Require that all code is reviewed by a separate person than the author. This will help eliminate rogue actors from introducing intentional or unintentional security bugs into your system.

**Static code analysis**  
When possible, leverage automation tools such as [Checkmarx](https://www.checkmarx.com), [Veracode](https://www.veracode.com/) and others to inspect code changes for security vulnerabilities.

**Test Dependencies**  
While it's common to think about vulnerabilities in your own code, most software today has a lot of dependencies. You should remember to check for vulnerabilities in all of your dependencies also. Depending on the language you are using, tools like [Snyk](https://www.snyk.io) are available to help automatically monitor and scan these.

**Dev environments**  
Your development environments should be isolated from production and staging systems. Each development environment should not be able to access production databases and resources. Any secrets that are required for your environment should be different in dev than in production or staging.

**Product architecture**  
Having a current product architecture document is a prerequisite for being able to think about product security. It's important to keep your product architecture documents current.

**Encryption Primitives**  
ensure that encryption methods are not “homegrown”. Use industry defined standards when encrypting data. Also, it's important to know your (potential) buyer. Common standards like RSA and AES are frequently accepted.

**Continuous threat modeling**  
Identify and document your trust boundaries and threat models in your system early. Continue to update these docs as your system evolves. Knowing where the trust boundaries are and where the biggest threat could come from will help you prioritize solutions.

**Feature security design reviews**  
All changes that have a design review should focus on a security review also. If you aren't an expert in security, bring an expert in who can show you where the weak points are and design a way to harden these before writing the new system.

**Secret Management**  
Your code should use a vault to store secrets when possible. Consider using [Hashicorp Vault](https://www.vaultproject.io/) or [Torus.sh](https://www.torus.sh/) for this.

**Application Security**  
Read the [OWASP Top 10 Vulnerabilities](https://www.veracode.com/directory/owasp-top-10), near the bottom of that page, labeled A1-A10, and think about how someone could use these vulnerabilities to gain access to your system, databases or network  

**Random Number Seed**  
Seed random number generators appropriately for the language you are using. Often, random numbers are used to create session ids or user ids. The UUID v4 format is random, and it's important to read the docs or code for your uuid library to determine if you are responsible for seeding.

## Product
----  
**Password security**  
Many applications require that users sign up and will have to store passwords to allow the user to log in again. You will have to be able to explain the following features around password security:  
- How are passwords stored? (bcrypt is a great answer, but make sure it's including a salt.)  
- Do you enforce a minimum password strength?  
- Do you have a configurable password expiration policy?  
- Do you prevent password reuse when changing a password?  
- How can a password be reset when needed?  
- Can a user enable a second factor login requirement?  
- Can an organization enforce 2 factor login for all users?  

**API Tokens**  
API Tokens are often treated less securely than passwords, but they are just as powerful as a logged in user. Treat tokens with the same level of security as you would passwords.

**Sessions**  
When an account is deleted or has a password changed, all existing sessions should be deleted.

**Client side**  
If your application is using cookies or local/session storage, ensure that all confidential data stored is in server-readable JWT tokens only.

**Secure defaults**  
Security shouldn't be a feature a user has to enable or opt into. Enforce secure defaults out of the box.

**Demonstrable security**  
Many enterprise buyers will ask you to provide documentation around your security efforts. Be prepared to show any of the following:
- Certifications
- Audits
- Penetration Test results
- Security Policies
- Security Forms
- White Papers

**Information Security Policy**  
Have a written and published Information Security Policy for how you will treat data and access to all data. Some good examples to start with are [Datadog](https://www.datadoghq.com/security/) or [Dropbox](https://www.dropbox.com/security). It's pretty common to have these hosted on a /security URL.

## Examples  
<DIV style="float:left">
<a href="/box/product-security"><img src="/box/images/example.png" width="300px" align="left" style="margin:0;"/></a>
<DIV class="clearfix"></DIV>
### [Box Product Security](/box/product-security)
</DIV>
