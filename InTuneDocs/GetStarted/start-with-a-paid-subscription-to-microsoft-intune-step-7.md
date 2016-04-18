---
title: Customize the company portal
ms.custom: na
ms.reviewer: na
ms.service: microsoft-intune
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid:
author: Staciebarker
---

# Customize the company portal
The [!INCLUDE[wit_iwportal_1](../includes/wit_iwportal_1_md.md)] is where users access company data and can do common tasks like enrolling devices, installing apps, and locating information for assistance from your IT department.

> [!TIP]
> When you customize the company portal, the configurations apply to both the company portal website and company portal apps.

Customizing the company portal helps provide a familiar and helpful experience for your end users. To do it, just log into the [Microsoft Intune administrator console](https://manage.microsoft.com) as a tenant or service administrator, choose **Admin** &gt; **Company Portal** and configure the company portal settings.

![alt text](./media/companyportal.png "Company portal settings in the ADMIN workspace of the Intune administration console")

## Company contact information and privacy statement
The company name is displayed as the company portal title. The contact information and details are displayed to users in the Contact IT screen of the company portal. The privacy statement is displayed when a user clicks on the privacy link.

|Field name|Max length|More information|
    |----------|------------------------|----------------|
    |Company name|40|This name is displayed as the title of the company portal.|
    |IT department contact name|40|This name is displayed on the **Contact IT** page.|
    |IT department phone number|20|This contact number is displayed on the **Contact IT** page.|
    |IT department email address|40|This contact address is displayed on the **Contact IT** page. You must enter a valid email address in the format **alias@domainname.com**.|
    |Additional information|120|Displayed on the **Contact IT** page.|
    |Company privacy statement URL|79|You can specify your own company privacy statement that appears when users click the privacy links from the company portal. You must enter a valid URL in the format **https://www.contoso.com**.|

## Support contacts
The support website is displayed to users in the company portal to enable them to access online support.

|Field name|Max length|More information|
    |----------|------------------------|----------------|
    |Support website URL|150|If you have a support website that you want your users to use, specify the URL here. The URL must be in the format **https://www.contoso.com**. If you don't specify a URL, nothing is displayed for the support website on the **Contact IT** page in the company portal.|
    |Website name|40|This name is the friendly name that is displayed for the URL to the support website. If you specify a support website URL and no friendly name, then **Go to IT website** is displayed on the **Contact IT** page in the company portal.|

## Company branding customization
You can customize your company portal with your company logo, company name, theme color and background.

|Field name|More information|
    |----------|----------------|
    |Theme color|Select a theme color to apply to the company portal.|
    |Include company logo|When you enable this option, you can upload your company logo to show in your company portal. You can upload two logos: one logo that is displayed when the company portal background is white, and one logo that is displayed when the company portal background uses your selected theme color. Each logo must be a .png or .jpg file type and have a maximum resolution of 400 x 100 pixels and be 750 KB or less in size.|
    |Choose a background for [!INCLUDE[win8_client_2](../includes/win8_client_2_md.md)] company portal app|This setting affects the background for the [!INCLUDE[win8_client_2](../includes/win8_client_2_md.md)] company portal app only.|


After you save your changes, you can use the links provided at the bottom of the **Company Portal** page of the administration console to view the company portal website. These links cannot be changed. When a user signs in, these links display your subscriptions in the company portal.

## Next steps
Congratulations! You have just completed step 7 of the *Get started with a paid subscription to Microsoft Intune* guide.
>[!div class="step-by-step"]

>[&larr; **Create policies and apps**](.\get-started-with-a-paid-subscription-to-microsoft-intune-step-6.md)       [**Enroll devices** &rarr;](.\get-started-with-a-paid-subscription-to-microsoft-intune-step-8.md)  