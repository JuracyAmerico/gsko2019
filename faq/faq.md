# Frequently Asked Questions

## General

### Does Tableau Server support multiple authentication schemes at the same time?

## Identity Stores

### Does Tableau Server support multiple identity stores at the same time?

## SAML

### What SAML profiles does Tableau support?

### Does Tableau support IdP initiated SAML?

### Does Tableau support Encrypted Assertions?

## OpenID Connect

### What OpenID Connect providers does Tableau support?

### What OpenID Connect profiles does Tableau support?

## SSL

## Encryption

## Reverse Proxies and Load Balancers

### Why would I configure a Reverse Proxy for Tableau Server?

Tableau Server actually includes a reverse proxy as part of its installation. The Gateway is a proxy server because it proxies traffic to the back end components of the instance like the Application Server or Vizportal. This is transparent to users and mostly to Tableau Admins so why add an external proxy?

A Reverse proxy can be used for several reasons:

- You want to define a public DNS name that points to the Tableau Server. This might be an external facing use case and the Tableau Server instance could be in an internal network zone.
- You have a multi-node Tableau instance with multiple Application Servers (gateways). In this case you want to direct the incoming traffic to each of the Application Servers. Note that the Application Servers will also perform load balancing to the other Tableau components so its not necessary to have a complex balancing scheme on the Load Balancer.
- The reverse proxy might be an authenticating proxy that will enable authentication of the user before they are allowed to access the Tableau Server. Google IAP is an example of such a proxy.
- The proxy might be a load balancer. Even if you are not load balancing traffic to more than one node you may know that you plan on doing this at a later date. Or you know that the Tableau Instance will change it's name.
- You might want to offload SSL to the proxy or load Balancer.