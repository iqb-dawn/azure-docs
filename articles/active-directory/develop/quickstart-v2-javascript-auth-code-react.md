---
title: "Quickstart: Sign in users in JavaScript React single-page apps (SPA) with auth code and call Microsoft Graph | Azure"
titleSuffix: Microsoft identity platform
description: In this quickstart, learn how a JavaScript React single-page application (SPA) can sign in users of personal accounts, work accounts, and school accounts by using the authorization code flow and call Microsoft Graph.
services: active-directory
author: j-mantu
manager: CelesteDG

ms.service: active-directory
ms.subservice: develop
ms.topic: quickstart
ms.workload: identity
ms.date: 09/09/2021
ms.author: jamesmantu
ms.custom: aaddev, scenarios:getting-started, languages:JavaScript, devx-track-js
#Customer intent: As an app developer, I want to learn how to login, logout, conditionally render components to authenticated users, and acquire an access token for a protected resource such as Microsoft Graph by using the Microsoft identity platform so that my JavaScript React app can sign in users of personal accounts, work accounts, and school accounts.
---

# Quickstart: Sign in and get an access token in a React SPA using the auth code flow

In this quickstart, you download and run a code sample that demonstrates how a JavaScript React single-page application (SPA) can sign in users and call Microsoft Graph using the authorization code flow. The code sample demonstrates how to get an access token to call the Microsoft Graph API or any web API.

See [How the sample works](#how-the-sample-works) for an illustration.

## Prerequisites

* Azure subscription - [Create an Azure subscription for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
* [Node.js](https://nodejs.org/en/download/)
* [Visual Studio Code](https://code.visualstudio.com/download) or another code editor

> [!div renderon="docs"]
> ## Register and download your quickstart application
> To start your quickstart application, use either of the following options.
>
>
> ### Option 1 (Express): Register and auto configure your app and then download your code sample
>
> 1. Go to the <a href="https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade/quickStartType/ReactSpaQuickstartPage/sourceType/docs" target="_blank">Azure portal - App registrations</a> quickstart experience.
> 1. Enter a name for your application.
> 1. Under **Supported account types**, select **Accounts in any organizational directory and personal Microsoft accounts**.
> 1. Select **Register**.
> 1. Go to the quickstart pane and follow the instructions to download and automatically configure your new application.
>
> ### Option 2 (Manual): Register and manually configure your application and code sample
>
> #### Step 1: Register your application
>
> 1. Sign in to the <a href="https://portal.azure.com/" target="_blank">Azure portal</a>.
> 1. If you have access to multiple tenants, use the **Directory + subscription** filter :::image type="icon" source="./media/common/portal-directory-subscription-filter.png" border="false"::: in the top menu to switch to the tenant in which you want to register the application.
> 1. Search for and select **Azure Active Directory**.
> 1. Under **Manage**, select **App registrations** > **New registration**.
> 1. When the **Register an application** page appears, enter a name for your application.
> 1. Under **Supported account types**, select **Accounts in any organizational directory and personal Microsoft accounts**.
> 1. Select **Register**. On the app **Overview** page, note the **Application (client) ID** value for later use.
> 1. Under **Manage**, select **Authentication**.
> 1. Under **Platform configurations**, select **Add a platform**. In the pane that opens select **Single-page application**.
> 1. Set the **Redirect URIs** value to `http://localhost:3000/`. This is the default port NodeJS will listen on your local machine. We’ll return the authentication response to this URI after successfully authenticating the user.
> 1. Select **Configure** to apply the changes.
> 1. Under **Platform Configurations** expand **Single-page application**.
> 1. Confirm that under **Grant types** ![Already configured](media/quickstart-v2-javascript/green-check.png) Your Redirect URI is eligible for the Authorization Code Flow with PKCE.

> [!div class="sxs-lookup" renderon="portal"]
> #### Step 1: Configure your application in the Azure portal
> For the code sample in this quickstart to work, add a **Redirect URI** of `http://localhost:3000/`.
> > [!div renderon="portal" id="makechanges" class="nextstepaction"]
> > [Make these changes for me]()
>
> > [!div id="appconfigured" class="alert alert-info"]
> > ![Already configured](media/quickstart-v2-javascript/green-check.png) Your application is configured with these attributes.

#### Step 2: Download the project

> [!div renderon="docs"]
> To run the project with a web server by using Node.js, [download the core project files](https://github.com/Azure-Samples/ms-identity-javascript-react-spa/archive/main.zip).

> [!div renderon="portal" class="sxs-lookup"]
> Run the project with a web server by using Node.js

> [!div renderon="portal" class="sxs-lookup" id="autoupdate" class="nextstepaction"]
> [Download the code sample](https://github.com/Azure-Samples/ms-identity-javascript-react-spa/archive/main.zip)

> [!div renderon="docs"]
> #### Step 3: Configure your JavaScript app
>
> In the *src* folder, open the *authConfig.js* file and update the `clientID`, `authority`, and `redirectUri` values in the `msalConfig` object.
>
> ```javascript
> /**
> * Configuration object to be passed to MSAL instance on creation.
> * For a full list of MSAL.js configuration parameters, visit:
> * https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/configuration.md
> */
> export const msalConfig = {
>    auth: {
>        clientId: "Enter_the_Application_Id_Here",
>        authority: "Enter_the_Cloud_Instance_Id_Here/Enter_the_Tenant_Info_Here",
>        redirectUri: "Enter_the_Redirect_Uri_Here"
>    },
>    cache: {
>        cacheLocation: "sessionStorage", // This configures where your cache will be stored
>        storeAuthStateInCookie: false, // Set this to "true" if you are having issues on IE11 or Edge
>    },
> ```

> [!div renderon="portal" class="sxs-lookup"]
> > [!NOTE]
> > `Enter_the_Supported_Account_Info_Here`

> [!div renderon="docs"]
>
> Modify the values in the `msalConfig` section as described here:
>
> - `Enter_the_Application_Id_Here` is the **Application (client) ID** for the application you registered.
>
>    To find the value of **Application (client) ID**, go to the app registration's **Overview** page in the Azure portal.
> - `Enter_the_Cloud_Instance_Id_Here` is the instance of the Azure cloud. For the main or global Azure cloud, enter `https://login.microsoftonline.com`. For **national** clouds (for example, China), see [National clouds](authentication-national-cloud.md).
> - `Enter_the_Tenant_info_here` is set to one of the following:
>   - If your application supports *accounts in this organizational directory*, replace this value with the **Tenant ID** or **Tenant name**. For example, `contoso.microsoft.com`.
>
>    To find the value of the **Directory (tenant) ID**, go to the app registration's **Overview** page in the Azure portal.
>   - If your application supports *accounts in any organizational directory*, replace this value with `organizations`.
>   - If your application supports *accounts in any organizational directory and personal Microsoft accounts*, replace this value with `common`. **For this quickstart**, use `common`.
>   - To restrict support to *personal Microsoft accounts only*, replace this value with `consumers`.
>
>    To find the value of **Supported account types**, go to the app registration's **Overview** page in the Azure portal.
> - `Enter_the_Redirect_Uri_Here` is `http://localhost:3000/`.
>
> The `authority` value in your *authConfig.js* should be similar to the following if you're using the main (global) Azure cloud:
>
> ```javascript
> authority: "https://login.microsoftonline.com/common",
> ```
>
> [!div class="sxs-lookup" renderon="portal"]
> #### Step 3: Your app is configured and ready to run
> We have configured your project with values of your app's properties.

> [!div renderon="docs"]
>
> Scroll down in the same file and update the `graphMeEndpoint`.
> - Replace the string `Enter_the_Graph_Endpoint_Herev1.0/me` with `https://graph.microsoft.com/v1.0/me`
> - `Enter_the_Graph_Endpoint_Herev1.0/me` is the endpoint that API calls will be made against. For the main (global) Microsoft Graph API service, enter `https://graph.microsoft.com/` (include the trailing forward-slash). For more information, see the [documentation](/graph/deployments).
>
>
>
> ```javascript
>   // Add here the endpoints for MS Graph API services you would like to use.
>    export const graphConfig = {
>        graphMeEndpoint: "Enter_the_Graph_Endpoint_Herev1.0/me"
>    };
> ```
>
>
#### Step 4: Run the project

Run the project with a web server by using Node.js:

1. To start the server, run the following commands from within the project directory:
    ```console
    npm install
    npm start
    ```
1. Browse to `http://localhost:3000/`.

1. Select **Sign In** to start the sign-in process and then call the Microsoft Graph API.

    The first time you sign in, you're prompted to provide your consent to allow the application to access your profile and sign you in. After you're signed in successfully, click on the **Request Profile Information** to display your profile information on the page.

## More information

### How the sample works

![Diagram showing the authorization code flow for a single-page application.](media/quickstart-v2-javascript-auth-code/diagram-01-auth-code-flow.png)

### msal.js

The MSAL.js library signs in users and requests the tokens that are used to access an API that's protected by the Microsoft identity platform.

If you have Node.js installed, you can download the latest version by using the Node.js Package Manager (npm):

```console
npm install @azure/msal-browser @azure/msal-react
```

## Next steps

Next, try a step-by-step tutorial to learn how to build a React SPA from scratch that signs in users and calls the Microsoft Graph API to get user profile data:

> [!div class="nextstepaction"]
> [Tutorial: Sign in users and call Microsoft Graph](tutorial-v2-react.md)
