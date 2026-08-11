![](data:image/png;base64...)

# Operational Guide: Glasgow TRE Data Transfer Service Access

Contents

[Operational Guide: Glasgow TRE Data Transfer Service Access 1](#_Toc235092210)

[INTRODUCTION 1](#_Toc235092211)

[SECTION 1 - SYSTEM PREREQUISITES AND INITIAL ACCESS 2](#_Toc235092212)

[1.1 – Connection Details 2](#_Toc235092213)

[1.2 – Credential Management 2](#_Toc235092214)

[SECTION 2 – FIRST-TIME CONFIGURATION AND TWO-FACTOR AUTHENTICATION (2FA) SETUP 2](#_Toc235092215)

[2.1 – Service and Protocol Selection 3](#_Toc235092216)

[2.2 – Authenticator Application Registration 3](#_Toc235092217)

[2.3 – Verification and Time Sensitivity 3](#_Toc235092218)

[2.4 – Manual Code Entry 4](#_Toc235092219)

[SECTION 3 – STANDARD LOGIN PROCEDURE (SUBSEQUENT SESSIONS) 4](#_Toc235092220)

[SECTION 4 – FILE MANAGEMENT OPERATIONS 5](#_Toc235092221)

[4.1 – Directory Navigation 5](#_Toc235092222)

[4.2 – Uploading Data 6](#_Toc235092223)

[4.3 – File Manipulation 6](#_Toc235092224)

[SECTION 5 – INTERFACE CUSTOMISATION AND SESSION MANAGEMENT 7](#_Toc235092225)

[5.1 – Display Mode 7](#_Toc235092226)

[5.2 – Secure Logout 7](#_Toc235092227)

[SECTION 6 – SUPPORT AND INCIDENT REPORTING 7](#_Toc235092228)

[6.1 - Alternative Contact Method 8](#_Toc235092229)

## INTRODUCTION

This document provides an operational guide for accessing and using the Glasgow TRE DataTransfer Service. It describes how to connect to the secure file transfer environment, configure two-factor authentication (2FA), manage files, and obtain support. This guide should be read by all new users prior to accessing the service.

## SECTION 1 - SYSTEM PREREQUISITES AND INITIAL ACCESS

### 1.1 – Connection Details

To access the secure file transfer environment, users must navigate to the following specific endpoint:

URL: ?<http://sftp.glasgowtre.ac.uk:2022/>

![](data:image/png;base64...)

### 1.2 – Credential Management

**Username:** Users will be provided with a username in the welcome email.

**Initial Password:** Users will be issued a permanent password via a separate communication channel.

**Restriction:** Self-service password modification is disabled. The system does not allow users to change their own passwords.

**Action Required:** If you forget your password or encounter login failures, you must contact us via [the UofG Helpdesk](https://milngavie.cent.gla.ac.uk/idp/profile/SAML2/Redirect/SSO?execution=e1s2) portal as per the instructions in section 6. Please do not attempt to bypass security protocols.

## SECTION 2 – FIRST-TIME CONFIGURATION AND TWO-FACTOR AUTHENTICATION (2FA) SETUP

Upon your first successful login with the provided credentials, you will be directed to the configuration dashboard. Follow these steps strictly to enable secure access.

![](data:image/png;base64...)

### 2.1 – Service and Protocol Selection

Step1. Locate the **Configuration** section on the main dashboard.

Step 2. Find the **dropdown** menu.

Step 3. Selection: Choose **GlasgowTRE (DataTransfer Service)**.

Step 4. Find the dropdown menu labelled **Require 2FA**.

Step 5. Selection: Choose **HTTP**.

Step 6. Click the Enable button to apply these settings.

### 2.2 – Authenticator Application Registration

Immediately after enabling, the system will generate a dynamic QR code for 2FA enrolment.

**Prepare Device**: Unlock your mobile device and open your Authenticator Application (e.g., Microsoft Authenticator) and **scan the QR Code**:

Once scanned, a new entry will appear in the Microsoft Authenticator named GlasgowTRE (DataTransfer Service) with a one-time password code – a 6-digit code authenticator.

Step 3. Please enter the code in the **Authentication Code** section.

### 2.3 – Verification and Time Sensitivity

**Critical Timing Constraint**: These codes are time-synchronised and expire every 30 seconds.

**Action**: Immediately enter the current 6-digit code into the verification field on the web interface.

**Warning**: If the code expires before entry, wait for the next cycle and enter the new code. Do not reuse old codes.

Upon successful validation, your account is fully configured for future logins.

**Warning**: If your primary authenticator device is lost, damaged, or inaccessible, don't hesitate to get in touch with us as outlined in section 6.

### 2.4 – Manual Code Entry or for Non-Microsoft and Non-University Account Holders.

If you are using a personal account outside of Microsoft or University ecosystems, or if the QR code fails to scan, becomes unreadable, or is simply incompatible with your device, manual entry is the recommended solution.

Step-by-Step Instructions

Step 1. Download and Open Microsoft Authenticator (Apple App Store (iOS) or Google Play Store (Android)

Step 2. Launch the app and sign in with your personal Microsoft account credentials if prompted.

Step 3. Tap the + (Plus) icon or "Add Account" button to begin setting up a new entry.

Step 4. Press the scan icon at the bottom of your Microsoft Authenticator.

Step 5. Click on 'Enter code manually'.

Step 6. Click on 'Other (Google, Facebook, etc)'.

Step 7. On the Add account page, add Account Name, preferably: Glasgow TRE.

Step 8. On the Secret Key section, add the code provided on the screen.

A new entry will appear on the Microsoft Authenticator named GlasgowTRE (DataTransfer Service) with a one-time password code – a 6-digit code authenticator to be used.

Please enter the code in the Authentication Code section.

**Warning**: In case the screen has been left open for a long period of time, please refresh the screen and try the above steps again, as it will show a fail message when entering the code.

Please be advised that you have the option to generate a Secret Key at any time within the system by pressing the 'Generate new secret key' button.

![](data:image/png;base64...)

## SECTION 3 – STANDARD LOGIN PROCEDURE (SUBSEQUENT SESSIONS)

For all sessions following the initial setup, the authentication flow requires your static password. Upon clicking **'Sign In**,' you will then be prompted to provide the authentication code generated by the 'GlasgowTRE (DataTransfer Service)' entry in your Microsoft Authenticator app.

![](data:image/png;base64...)

## SECTION 4 – FILE MANAGEMENT OPERATIONS

Once logged in, the interface allows for secure data handling.

### 4.1 – Directory Navigation

**Default View:** Upon login, click on the Files section.

![](data:image/png;base64...)

**Folder Creation:** If no directory exists and you want to create a folder:

Step 1. Click the New Folder button.

Step 2. Assign a descriptive name to the folder.

Step 3. Confirm creation by pressing the tick button

![](data:image/png;base64...)

### 4.2 – Uploading Data

Step 1. Navigate to the target folder (create one if necessary).

Step 2. Initiate the upload process (typically via clicking ‘Drop files or folders here or click to upload or by clicking ‘Browse folder’).

Step 3. Select the files from your local machine.

Step 4. Press ‘Save’

### 4.3 – File Manipulation

Users have full control over their uploaded assets. Available actions include:

**Preview:** Click the **Eye Icon** next to a file to view its contents directly in the browser (if supported by the file type).

![](data:image/png;base64...)

**Rename:** Select the rename option to rename the files.

**Deletion:** Select the delete option to permanently remove files.

**Organisation:** Use Move or Copy functions to relocate files between folders.

![](data:image/png;base64...)

## SECTION 5 – INTERFACE CUSTOMISATION AND SESSION MANAGEMENT

### 5.1 – Display Mode

The interface supports three visual themes to suit user preferences or lighting conditions. To select your preferred display mode, select that half-moon icon in the top-right corner of the screen to choose from **Light Mode** for standard high-contrast, **Dark Mode** for low-light optimisation, or **Auto** to switch automatically based on your system settings via the settings menu.

### 5.2 – Secure Logout

To ensure data security, locate the User Profile Icon in the top-right corner, click it to open the dropdown menu, select **Sign Out**, and verify that you are returned to the login screen.

## SECTION 6 – SUPPORT AND INCIDENT REPORTING

If you experience technical difficulties, encounter error messages, or require assistance with password resets, please follow the official reporting protocol below.

 UofG [Helpdesk](https://glasgow.saasiteu.com/Modules/SelfService/#serviceCatalog/filter/23b64fbdbd7d43fe8b9133457a9b8a8d)  *Service Catalogue ? UofG Helpdesk ? Report Something ? Glasgow TRE Helpdesk and Technical Support*. You may also locate this more readily by searching for "TRE" within the Service Catalogue, where you will find us, as per the image below:

![](data:image/png;base64...)

Log your email address and choose the category "Data (incl. Data ingress/extraction)". If you can, please include your project ID and confirm the datasets you will be making available to transfer; this will allow our technical team to provide you with the credentials you need for the agreed SFTP transfer.

### 6.1 - Alternative Contact Method

For urgent matters, non-University staff, or if the online catalogue is unavailable, contact the team directly via email:

Email Address: tre@glasgow.ac.uk
