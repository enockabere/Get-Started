<!-- @format -->

# MICROSOFT SINGLE SIGN ON

To configure permissions in Azure Active Directory (Azure AD) so that you can access user details, you need to grant the necessary permissions to your application registration.

## Azure AD App Permissions

First, you need to register your Django application with Azure Active Directory (Azure AD). Here are the steps to grant the necessary permissions to your application:

### Go to the Azure portal (https://portal.azure.com/).

### Navigate to Azure AD

- In the left-hand menu, select `Azure Active Directory`

### App Registrations

- Click on `App registrations` (or `App registrations(Preview)` if that's what you see).

### Select Your App

- Click on the name of your application registration to which you want to grant permissions.

### API Permissions

- In the left-hand menu, under `Manage`, select `API permissions`.

### Add a Permission

- Click on the `+ Add a permission` button to add a new permission.

### Microsoft APIs

- Select `Microsoft APIs`

### Select API

- Choose the Microsoft API for which you want to grant permissions. For user details, you typically need the Microsoft Graph API. Select `Microsoft Graph`

### Select Permissions

- Choose the permissions your application needs. To access user details, you might need `User.Read`, `User.Read.Basic.All` or other relevant permissions. These permissions grant access to user data. Click the checkbox next to the permissions you need.

### Grant Admin Consent

- After selecting the permissions, you will need to grant admin consent for these permissions to be effective. Click the `Grant admin consent` button, and an administrator will be prompted to approve these permissions.

### Grant User Consent (if required)

- Depending on your Azure AD settings, you might also need to grant user consent. Users will be prompted to consent when they sign in and use the application.

### API Permissions Page

- After granting consent, you should see the permissions listed on the `API permissions` page for your application.

### Save Changes

- Don't forget to save your changes.

### Summary

Go to `Add Permissions` > then select `Microsoft Graph ` > then click `Delegated Permissions` > click on `email` and `profile` checkboxes > search `user` to set permissions for users > click on `User.Read` and `User.Read.Basic.All` checkboxes to add the permissions > click on `Add Permission` button to save the changes > Grant `admin consent` to `User.Read.All`
