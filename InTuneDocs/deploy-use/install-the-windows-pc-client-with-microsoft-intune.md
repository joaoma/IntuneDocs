---

# required metadata

title: Install the PC client software | Microsoft Docs
description: Use this guide to help you get your Windows PCs managed by the Microsoft Intune client software.
keywords:
author: staciebarker
ms.author: stabar
ms.date: 02/14/2017
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 64c11e53-8d64-41b9-9550-4b4e395e8c52

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: owenyen
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Install the Intune software client on Windows PCs
Windows PCs can be enrolled by installing the Intune client software. The Intune client software can be installed by using the following methods:

- By the IT admin, using one of these methods: manual installation, Group Policy, or installation included in a disk image

- By end users, who manually install the client software

The Intune client software contains the minimum software necessary to enroll the PC in Intune management. After a PC has been enrolled, the Intune client software then downloads the full client software required for PC management.

This series of downloads reduces the impact on the network's bandwidth and minimizes the time required to initially enroll the PC in Intune. It also ensures that the client has the most recent software available after the second download has finished.

## Download the Intune client software

All methods, except those in which users install the Intune client software themselves, require that IT admins download the software first so that it can be subsequently deployed to end users.

1.  In the [Microsoft Intune administration console](https://manage.microsoft.com/), click **Admin** &gt; **Client Software Download**.

  ![Download the Intune PC client](../media/pc-sa-client-download.png)

2.  On the **Client Software Download** page, click **Download Client Software**. Then save the **Microsoft_Intune_Setup.zip** package that contains the software to a secure location on your network.

The Intune client software installation package contains unique and specific information, which is available through an embedded certificate, about your account. If unauthorized users gain access to the installation package, they can enroll PCs to the account that is represented by its embedded certificate and might gain access to company resources.

3.  Extract the contents of the installation package to the secure location on your network.

    > [!IMPORTANT]
    > Do not rename or remove the **ACCOUNTCERT** file that is extracted, or the client software installation will fail.

## Deploy the client software manually

On the computer(s) on which the client software is going to be installed, go to the folder where the client software installation files are located. Then run **Microsoft_Intune_Setup.exe** to install the client software.

> [!NOTE]
> The status of the installation is displayed when you hover over the icon in the taskbar on the client PC.

## Deploy the client software by using Group Policy

1.  In the folder that contains the files **Microsoft_Intune_Setup.exe** and **MicrosoftIntune.accountcert**, run the following command to extract the Windows Installer-based installation programs for 32-bit and 64-bit computers:

    ```
    Microsoft_Intune_Setup.exe/Extract <destination folder>
    ```

2.  Copy the **Microsoft_Intune_x86.msi** file, the **Microsoft_Intune_x64.msi** file, and the **MicrosoftIntune.accountcert** file to a network location that can be accessed by all computers on which the client software is going to be installed.

    > [!IMPORTANT]
    > Do not separate or rename the files or the client software installation will fail.

3.  Use Group Policy to deploy the software to computers on your network.

    For more information about how to use Group Policy to automatically deploy software, see [Group Policy for Beginners](https://technet.microsoft.com/library/hh147307.aspx).

## Deploy the client software as part of an image
You can deploy the Intune client software to computers as part of an operating system image by using the following procedure as a guide:

1.  Copy the client installation files, **Microsoft_Intune_Setup.exe** and **MicrosoftIntune.accountcert**, to the **%Systemdrive%\Temp\Microsoft_Intune_Setup** folder on the reference computer.

2.  Create the **WindowsIntuneEnrollPending** registry entry by adding the following command to the **SetupComplete.cmd** script:

    ```
    %windir%\system32\reg.exe add HKEY_LOCAL_MACHINE\Software\Microsoft\Onlinemanagement\Deployment /v
    WindowsIntuneEnrollPending /t REG_DWORD /d 1
    ```

3.  Add the following command to **setupcomplete.cmd** to run the enrollment package with the /PrepareEnroll command-line argument:

    ```
    %systemdrive%\temp\Microsoft_Intune_Setup\Microsoft_Intune_Setup.exe /PrepareEnroll
    ```
    > [!TIP]
    > The **SetupComplete.cmd** script enables Windows Setup to make modifications to the system before a user signs on. The **/PrepareEnroll** command-line argument prepares a targeted computer to be automatically enrolled in Intune after Windows Setup finishes.

4.  Put **SetupComplete.cmd** in the **%Windir%\Setup\Scripts** folder on the reference computer.

5.  Capture an image of the reference computer and then deploy this to targeted computers.

    When the targeted computer restarts at the completion of Windows Setup, the **WindowsIntuneEnrollPending** registry key is created. The enrollment package checks to see if the computer is enrolled. If the computer is enrolled, no further action is taken. If the computer is not enrolled, the enrollment package creates a Microsoft Intune Automatic Enrollment Task.

    When the automatic enrollment task runs at the next scheduled time, it checks the existence of the **WindowsIntuneEnrollPending** registry value, and it tries to enroll the targeted PC in Intune. If the enrollment fails for any reason, the enrollment is retried the next time the task runs. The retries continue for a month.

    The Intune Automatic Enrollment Task, the **WindowsIntuneEnrollPending** registry value, and the account certificate are deleted from the targeted computer either when the enrollment is successful or after a month (whichever comes first).

## Instruct users to self-enroll

Users install the Intune client software by going to the [Company Portal website](http://portal.manage.microsoft.com). The exact information that users see in the web portal varies, depending on your account's MDM Authority and the OS platform/version of the user's PC. 

If users haven't been assigned an Intune license or if the organization's MDM Authority hasn't been set to Intune, users aren't shown any options to enroll.

If users have been assigned an Intune license, and the organization's MDM Authority has been set to Intune:

- Windows 7 or Windows 8 PC users are shown ONLY the option to enroll to Intune by downloading and installing the PC client software that is unique to their organization.

- Windows 10 or Windows 8.1 PC users are shown two enrollment options:

  -  **Enroll PC as a mobile device**: Users choose the **Find Out How to Enroll** button and are taken to instructions on how to enroll their PC as a mobile device. This button is prominently displayed, because MDM enrollment is considered to be the default and preferred enrollment option. However, the MDM option is not applicable to this topic, which covers only the client software installation.
  - **Enroll PC using the Intune client software**: You'll need to tell your users to select the **Click here to download it** link, which takes them through the client software installation.

The following table summarizes the options.

  ![Default enrollment options per platform](../media/default-enrollment-options-table.png)

The following screenshots show what users see as they enroll their devices using the software client.

Users are first prompted to identify or to enroll their device.

  ![identify or enroll device](../media/identify-device-or-enroll.png)

To have your users install the PC client software, you'll need to tell them to select the **Click here to download it** link, which enables users to download the PC client software and takes them through the installation process. The **Find out how to enroll** button takes users to documentation about how to enroll using MDM enrollment, which is not relevant to these software client instructions.

  ![choose Click here to download it link](../media/enroll-your-windows-device.png)

When users click the link, they see a **Download Software** button, which they select to start the PC client software installation.

  ![choose Download Software button](../media/download-pc-client-software.png)

Users are then asked to sign in with their corporate credentials.

  ![Sign in with your credentials](../media/sign-in-to-intune.png)

Users are taken to the Welcome page for the installation.

  ![Welcome page for PC client installation](../media/welcome-to-pc-agent-install-wizard.png)

Users choose **Next**, and the installation starts.

  ![Welcome page for PC client installation](../media/welcome-to-pc-agent-install-wizard.png)

When the installation completes, users choose **Finish**.

  ![Finish the PC client installation](../media/completed-the-setup-wizard.png)

If users try to enroll their PC as a mobile device after having already enrolled using the Intune PC client software, they see the following error screen.

  ![Screen shown if PC already enrolled](../media/page-shown-if-pc-already-enrolled.png)

## Monitor and validate successful client deployment
Use one of the following procedures to help you monitor and validate successful client deployment.

### To verify the installation of the client software from the Microsoft Intune administrator console

1.  In the [Microsoft Intune administration console](https://manage.microsoft.com/), click **Groups** &gt; **All Devices** &gt; **All Computers**.

2.  In the list, find the computers that are communicating with Intune, or search for a specific managed computer by typing the computer name (or any part of the name) in the **Search devices** box.

3.  Examine the status of the computer in the bottom pane of the console. Resolve any errors.

### To create a computer inventory report to display all enrolled computers

1.  In the [Microsoft Intune administration console](https://manage.microsoft.com/), click **Reports** &gt; **Computer Inventory Reports**.

2.  On the **Create New Report** page, leave the default values in all fields (unless you want to apply filters), and then click **View Report**.

3.  The **Computer Inventory Report** page opens in a new window that displays all computers that are successfully enrolled in Intune.

    > [!TIP]
    > Click any column heading in the report to sort the list by the contents of that column.


### See also
[Manage Windows PCs with Microsoft Intune](manage-windows-pcs-with-microsoft-intune.md)
[Troubleshoot client setup](../troubleshoot/troubleshoot-client-setup-in-microsoft-intune.md)
