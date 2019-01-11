# Glossary of Security and IAM Terms for Tableau

Below are common terms used in Tableau and IdP configurations and documentation.

### Identity and Access Management (IAM)

A security and business discipline that "enables the right individuals to access the right resources at the right times and for the right reasons". It addresses the need to ensure appropriate access to resources across increasingly heterogeneous technology environments and to meet increasingly rigorous compliance requirements.

### SAML 2.0

 Version 2 of the Security Assertion Markup Language (almost always referred to as SAML); a standard for exchanging authentication and authorization data between security domains.

### Single-Sign-On (SSO)

Refers to a broad spectrum of methods, standards, and specifications all of which ultimately facilitate a user's ability to log into various services by leveraging existing credentials from another service.Identity Provider (IdP) – refers broadly to the functionality, frameworks, and infrastructures that collectively work to provide the authorization and authentication services.

### System for Cross-domain Identity Management (SCIM)

A standard for automating the exchange of user identity information between identity domains, or IT systems.

### Service Provider (SP)

In the context of SAML, refers to products (including SaaS) which provide some utility to users, and require authorization and authentication services from an identity provider.

### Identity Provider (IdP)

The authority that verifies and asserts a user's identity and access to a requested resource (the "Service Provider")

### SP initiated SSO

When the login workflow starts at the SP (any product) and the user is redirected to the IdP to get authorization, it's referred to as SP initiated SSO, since the SP explicitly triggers the SSO workflow.
IdP initiated SSO – also referred to as unsolicited login; this is a method of triggering a SAML login to an SP from the IdP directly. 

### Assertion

A package of information that supplies one or more statements made by a SAML authority (usually the IdP). Typically, an assertion will contain details about the authorization details of the user in question, various relevant attributes associated to that user, and an authorization decision as to whether or not the user was authorized.

### Claim Rules

When establishing a trust relationship between an IdP and SP, the IdP needs to be told what user attributes the SP will need in the assertion, in order to be able to grant the user access. These attributes are collectively referred to claim rules.

### Signing Certificate

A digital certificate, which contains the public key used to sign messages by SPs and IdPs so that the counter party can verify that the messages are in fact originating from the trusted source, and not some malicious 3rd party impersonating one of them.

### Encryption Certificate

A digital certificate, which contains the public key used to encrypt the SAML requests/responses between SPs and IdPs so that the messages can't be read if intercepted in transit by malicious 3rd party.

### Federation Metadata URL

Some IdPs will generate a URL which a SP can use to auto-configure all, if not most, of the SAML settings needed to connect to it. In some cases, this may be an XML file, and not a URL.

### Relying Party Trust Metadata URL

When you enable SAML, your account will have a URL which your IdP can use to auto-configure all of our SAML settings. This URL contains the certificates, endpoints, and other information necessary for the IdP to communicate with the application.

### Assertion Consumer Service  (ACS)

An Assertion Consumer Service (or ACS) is SAML terminology for the location at a ServiceProvider that accepts SAML response messages (or SAML artifacts) for the purpose of establishing a session based on an assertion. It refers to an HTTP resource (often a virtual one) on a web site that processes SAML protocol messages and returns a cookie representing the information extracted from the message.

### Entity ID

A globally unique name for an Identity Provider or a Service Provider.