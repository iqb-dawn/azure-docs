---
title: 'Tutorial: Azure Active Directory single sign-on (SSO) integration with Visibly | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Visibly.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 09/02/2021
ms.author: jeedes
---

# Tutorial: Azure Active Directory single sign-on (SSO) integration with Visibly

In this tutorial, you'll learn how to integrate Visibly with Azure Active Directory (Azure AD). When you integrate Visibly with Azure AD, you can:

* Control in Azure AD who has access to Visibly.
* Enable your users to be automatically signed-in to Visibly with their Azure AD accounts.
* Manage your accounts in one central location - the Azure portal.

## Prerequisites

To get started, you need the following items:

* An Azure AD subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/free/).
* Visibly single sign-on (SSO) enabled subscription.

## Scenario description

In this tutorial, you configure and test Azure AD SSO in a test environment.

* Visibly supports **SP** initiated SSO.
* Visibly supports [Automated user provisioning](visibly-provisioning-tutorial.md).

## Add Visibly from the gallery

To configure the integration of Visibly into Azure AD, you need to add Visibly from the gallery to your list of managed SaaS apps.

1. Sign in to the Azure portal using either a work or school account, or a personal Microsoft account.
1. On the left navigation pane, select the **Azure Active Directory** service.
1. Navigate to **Enterprise Applications** and then select **All Applications**.
1. To add new application, select **New application**.
1. In the **Add from the gallery** section, type **Visibly** in the search box.
1. Select **Visibly** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure and test Azure AD SSO for Visibly

Configure and test Azure AD SSO with Visibly using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between an Azure AD user and the related user in Visibly.

To configure and test Azure AD SSO with Visibly, perform the following steps:

1. **[Configure Azure AD SSO](#configure-azure-ad-sso)** - to enable your users to use this feature.
    1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with B.Simon.
    1. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable B.Simon to use Azure AD single sign-on.
1. **[Configure Visibly SSO](#configure-visibly-sso)** - to configure the single sign-on settings on application side.
    1. **[Create Visibly test user](#create-visibly-test-user)** - to have a counterpart of B.Simon in Visibly that is linked to the Azure AD representation of user.
1. **[Test SSO](#test-sso)** - to verify whether the configuration works.

## Configure Azure AD SSO

Follow these steps to enable Azure AD SSO in the Azure portal.

1. In the Azure portal, on the **Visibly** application integration page, find the **Manage** section and select **single sign-on**.
1. On the **Select a single sign-on method** page, select **SAML**.
1. On the **Set up single sign-on with SAML** page, click the pencil icon for **Basic SAML Configuration** to edit the settings.

   ![Edit Basic SAML Configuration](common/edit-urls.png)

1. On the **Basic SAML Configuration** section, enter the values for the following fields:

    a. In the **Sign-on URL** text box, type the URL: 
    `https://app.visibly.io/`

	b. In the **Reply URL** text box, type the URL: `https://api.visibly.io/api/v1/verifyResponse`

1. Visibly application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

	![image](common/default-attributes.png)

1. In addition to above, Visibly application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirements.
	
	| Name |  Source Attribute|
	| ----------- | --------- |
	| city | user.city |
	| lastName | user.surname |
	| state | user.state |
	| department | user.department |
	| email | user.mail |

1. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section,  find **Certificate (Base64)** and select **Download** to download the certificate and save it on your computer.

	![The Certificate download link](common/certificatebase64.png)

1. On the **Set up Visibly** section, copy the appropriate URL(s) based on your requirement.

	![Copy configuration URLs](common/copy-configuration-urls.png)

### Create an Azure AD test user

In this section, you'll create a test user in the Azure portal called B.Simon.

1. From the left pane in the Azure portal, select **Azure Active Directory**, select **Users**, and then select **All users**.
1. Select **New user** at the top of the screen.
1. In the **User** properties, follow these steps:
   1. In the **Name** field, enter `B.Simon`.  
   1. In the **User name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
   1. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
   1. Click **Create**.

### Assign the Azure AD test user

In this section, you'll enable B.Simon to use Azure single sign-on by granting access to Visibly.

1. In the Azure portal, select **Enterprise Applications**, and then select **All applications**.
1. In the applications list, select **Visibly**.
1. In the app's overview page, find the **Manage** section and select **Users and groups**.
1. Select **Add user**, then select **Users and groups** in the **Add Assignment** dialog.
1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then click the **Select** button at the bottom of the screen.
1. If you're expecting any role value in the SAML assertion, in the **Select Role** dialog, select the appropriate role for the user from the list and then click the **Select** button at the bottom of the screen.
1. In the **Add Assignment** dialog, click the **Assign** button.

## Configure Visibly SSO

1. Sign in to Visibly using your credentials.

1. Navigate to the **Settings** option from the navigation menu.

	![Screenshot shows the settings option selected.](./media/visibly-tutorial/settings.png)

1. Click **Integrations** within Settings.

	![Screenshot shows Integrations selected from the Settings menu.](./media/visibly-tutorial/integrations.png)

1. In the **Integrations**, select **SSO**.

	![Screenshot shows S S O selected from the Integrations.](./media/visibly-tutorial/sso.png)

1. Perform the following steps in the following page.

	![Screenshot shows S S O Integration page where you can enter the values described.](./media/visibly-tutorial/configuration.png)

	a. In the **Entity ID** textbox, paste the **Entity ID** value which you have copied from the Azure portal.

	b. In the **SSO url** textbox, paste the **Login URL** value which you have copied from the Azure portal.

	c. In the **SSO name** textbox, give any valid name.

	d. Open the downloaded **Certificate (Base64)** from the Azure portal into Notepad and paste the content into the **Certificate** textbox or you can also upload the **Certificate** by selecting the **Upload Certificate**.

	e. Click **Save**.

### Create Visibly test user

In this section, a user called B.Simon is created in Visibly. Visibly supports just-in-time user provisioning, which is enabled by default. There is no action item for you in this section. If a user doesn't already exist in Visibly, a new one is created after authentication.

Visibly also supports automatic user provisioning, you can find more details [here](./visibly-provisioning-tutorial.md) on how to configure automatic user provisioning.

## Test SSO 

In this section, you test your Azure AD single sign-on configuration with following options. 

* Click **Test this application** in Azure portal. This will redirect to Visibly Sign-on URL where you can initiate the login flow. 

* Go to Visibly Sign-on URL directly and initiate the login flow from there.

* You can use Microsoft My Apps. When you click the Visibly tile in the My Apps, this will redirect to Visibly Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](../user-help/my-apps-portal-end-user-access.md).

## Next steps

Once you configure Visibly you can enforce session control, which protects exfiltration and infiltration of your organization’s sensitive data in real time. Session control extends from Conditional Access. [Learn how to enforce session control with Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-aad).
