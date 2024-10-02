# Implementing SSO for Custom Applications with IBM Security Verify

![Proj Img](https://imgur.com/P5PkEbc.jpg) 

## Introduction

This project focuses on setting up single sign-on (SSO) for a custom application using IBM Security Verify. IBM Security Verify offers federated cloud-based SSO with connectors, supporting both Security Assertion Markup Language (SAML) and OpenID Connect (OIDC). In this tutorial, you’ll learn how to establish the necessary connection for your custom application using the OIDC SSO protocol.

OpenID Connect v1.0 and OAuth 2.0 are widely adopted standards due to their straightforward client-side implementations. For web applications, the Authorization code grant type is commonly used and well-supported. In this tutorial, we’ll utilize the Authorization code grant type. Here are the key components used in this project:

    IBM Security Verify: provides identity-as-a-service for every user including SSO and MFA.
    OpenID Connect: modern standard for web SSO adding an identity layer to the OAuth 2.0 standard.
    Security Assertion Markup Language (SAML): provides authentication for a user once and communicate that authentication to multiple applications.
    
## 1. Add a custom application

Let’s proceed with logging into IBM Security Verify. Navigate to the Applications tab and click “Add application.” We will choose Custom Application for this project.

![Add application](https://imgur.com/dSvmARm.jpg) 

On the Sign-on tab, configure the following:

    Name your app (e.g., “Tester App”).
    Set the Sign-on method to “OpenID Connect 1.0.”
    Specify the application URL (e.g., http://localhost:9080).
    For Grant types, select Authorization code.
    Unselect the option Require proof key for code exchange (PKCE) verification.
    For redirect URIs, enter http://localhost:9080/app/oidcclient/redirect/tutorial.
    
Click "Save" to save the configuration. 

![Name app](https://imgur.com/HCLmoXq.jpg) 

![config app](https://imgur.com/Xe4aL4r.jpg) 

Next, under Entitlements, select “Automatic access for all users and groups” as the Access Type, and click “Save.”

![access type](https://imgur.com/tJEjr12.jpg) 

Our application has been successfully created! 🎉

![config complete](https://imgur.com/1TLBDuz.jpg) 

## 2. Collect application information for confirguration
Now, let’s collect the necessary needed for future steps. On the Applications menu, select the row with the newly created Tester App, and click the Settings icon.

![settings](https://imgur.com/JfzGpT2.jpg) 

Notate the following:

    Client ID
    Client secret 
    Introspection_endpoint
    Authorization_endpoint
    Token_endpoint
    Userinfo_endpoint

![note clientid](https://imgur.com/M4EuwP0.jpg) 

We will gather the remaining codes from the provided link within the Sign-on tab, under the OpenID Connect single sign-on configuration section.

![note clientid](https://imgur.com/pVY00JN.jpg) 

![link to endpoints](https://imgur.com/NtvOU4G.jpg) 

![note endpoints](https://imgur.com/H0XaLGh.jpg) 

![note endpoints2](https://imgur.com/UM02kIy.jpg) 

Finally, open your terminal and run the following command to clone the GitHub repo:

    git clone https://github.com/IBM/open-liberty-security-verify-tutorial.git

Navigate to the config directory:

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

## 3. Successful Authorization

We were able to end this project with a successful authorized connection. 


![successful auth](https://imgur.com/kBiBgCH.jpg) 

## Conclusion
In this project, I successfully implemented Single Sign-On (SSO) for a custom application using IBM Security Verify. You learned how to configure the OpenID Connect client within Open Liberty to seamlessly integrate with IBM Security Verify.

## fin
