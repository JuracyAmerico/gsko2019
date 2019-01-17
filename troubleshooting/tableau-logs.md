# Tableau Logs for Troubleshooting SAML Authentication

This section provides information on which Tableau logs are the most useful for troubleshooting SAML and other authentication schemes. 

In most cases capturing Tableau logs and Fiddler traces is the most valuable troubleshooting approach from the Tableau side. Note that the IdP will sometimes provide some useful logging that can help point to the issue.

Which log depends on the type of Authentication scheme and what stage in the authentication flow configuration you have reached.

For most SAML issues the key log file is the vizportal log and it is most useful to enable debug logging before reproducing any issues. Debug logging in vizportal will allow you to see the SAML requests and responses and also more detailed messages about failures.