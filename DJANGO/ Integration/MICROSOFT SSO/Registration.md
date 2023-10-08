<!-- @format -->

# MICROSOFT SINGLE SIGN ON

To build the callback URL for integrating Microsoft Office 365 login with your Django application, you need to follow these steps:

## Azure AD App Registration

First, you need to register your Django application with Azure Active Directory (Azure AD). Here are the steps to do this:

- Go to the Azure portal (https://portal.azure.com/).

- Navigate to `Azure Active Directory`

- Under `App registrations`, click on `New registration` to create a new application registration.

- Provide a name for your application, and for the `Redirect URI`, specify the URL where Azure AD should redirect users after authentication. This URL should be a route in your Django application.

- After registration, you will receive an Application `(client) ID` and a Directory `(tenant) ID.` You'll need these values later.
