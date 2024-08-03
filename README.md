# Configure Custom App to Integrate with IBM Security Verify for SSO

<div align="center">
  <img src="https://store-images.s-microsoft.com/image/apps.46016.d3eacc69-6358-4a43-94d6-465eb39ca496.57ac5c5e-d47e-4cd6-a125-1d8c8f96001f.a7754481-5cd2-4645-a426-f32c45fcd298" height="360" alt="ibmsverify logo"  />
  <img width="108" />
</div>

## Introduction

This project focuses on setting up single sign-on (SSO) for a custom application using IBM Security Verify. IBM Security Verify offers federated cloud-based SSO with connectors, supporting both Security Assertion Markup Language (SAML) and OpenID Connect (OIDC). In this tutorial, you’ll learn how to establish the necessary connection for your custom application using the OIDC SSO protocol.

OpenID Connect v1.0 and OAuth 2.0 are widely adopted standards due to their straightforward client-side implementations. For web applications, the Authorization code grant type is commonly used and well-supported. In this tutorial, we’ll utilize the Authorization code grant type. Here are the key components used in this project:

    IBM Security Verify: provides identity-as-a-service for every user including SSO and MFA.
    OpenID Connect: modern standard for web SSO adding an identity layer to the OAuth 2.0 standard.
    Security Assertion Markup Language (SAML): provides authentication for a user once and communicate that authentication to multiple applications.
    
## Add a custom application 1

We begin this project with opening IBM Security Verify, clicking on the Applications tab, then Add application. 

We will then click on Custom Application

![Add application](https://imgur.com/dSvmARm.jpg) 

For this project we will name our app "Tester App". Click the Sign-on tab and configure the following:

    Enter a name for the app, such as Tester App.
    Select the Sign-on method as Open ID Connect 1.0.
    Enter the application URL as http://localhost:9080.
    For Grant types, choose Authorization code.
    Unselect the option Require proof key for code exchange (PKCE) verification.
    For redirect URIs, enter http://localhost:9080/app/oidcclient/redirect/tutorial.
    
Click Save to save the configuration. 

![Name app](https://imgur.com/HCLmoXq.jpg) 

![config app](https://imgur.com/Xe4aL4r.jpg) 

Moving on to the Entitlements select Automatic access for all users and groups as the Access Type and click Save

![access type](https://imgur.com/tJEjr12.jpg) 

Our application has been susscessfully created.
![config complete](https://imgur.com/1TLBDuz.jpg) 

## Collect application information for confirguration 2
On the Applications menu, select the row with the newly created Tester App, and click the Settings icon.

![settings](https://imgur.com/JfzGpT2.jpg) 

We will note the following for future steps in this process:

    Client
    Client secret 
    Introspection endpoint
    Authorization_endpoint
    Token_endpoint
    Userinfo_endpoint

![note clientid](https://imgur.com/5NzSjrp.jpg) 

We will gather the remaining codes from the provided link within the sign-on tab 

![link to endpoints](https://imgur.com/NtvOU4G.jpg) 

![note endpoints](https://imgur.com/ZtHyhwq.jpg) 

![note endpoints2](https://imgur.com/hpBBFYH.jpg) 

Using terminal, we will Run the following command to clone the GitHub repo:

    git clone https://github.com/IBM/open-liberty-security-verify-tutorial.git

We will then cd to the config directory:

    cd open-liberty-security-verify-tutorial/src/main/liberty/config

We will then edit and configure both the server.xml file and the verify.config file by editing the Client ID, Client secret, token_endpoint, and authorization_endpoint with the information we previously noted earlier.

    <openidConnectClient id="tutorial"
             signatureAlgorithm="RS256"
             httpsRequired="false"
             redirectToRPHostAndPort="http://localhost:9080/app"
             clientId="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
             clientSecret="xxxxxxxxxx"
             authorizationEndpointUrl="https://[tenant id].verify.ibm.com/v1.0/endpoint/default/authorize"
             tokenEndpointUrl="https://[tenant id].verify.ibm.com/v1.0/endpoint/default/token"></openidConnectClient>

![term cmds](https://imgur.com/Sy6iW6n.jpg)  

![editing nano](https://imgur.com/R9HEMYq.jpg)  

## Successful Authorization 3

In this process we were able to end this project with a successful authorization connection. 

![unauth](https://imgur.com/Uk1FDJW.jpg) 

![successful auth](https://imgur.com/kBiBgCH.jpg) 


## Conclusion
In this project, I was able to successfully add SSO to a custom application with IBM Security Verify. You saw how the OpenID Connect client is configured using the OpenID client on Open Liberty to work with IBM Security Verify.

## fin
