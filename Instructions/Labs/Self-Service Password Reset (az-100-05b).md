---
lab:
    title: 'Self-Service Password Reset'
    module: 'Implement and Manage Hybrid Identtities'
---

# Lab: Self-Service Password Reset
  
All tasks in this lab are performed from the Azure portal 

Lab files: none

### Scenario
  
Adatum Corporation wants to take advantage of Azure AD Premium features


### Objectives
  
After completing this lab, you will be able to:

- Manage Azure AD users and groups

- Manage Azure AD-integrated SaaS applications


### Exercise 1: Manage Azure AD users and groups

The main tasks for this exercise are as follows:

1. Create a new Azure AD tenant

1. Activate Azure AD Premium v2 trial

1. Create and configure Azure AD users

1. Assign Azure AD Premium v2 licenses to Azure AD users

1. Manage Azure AD group membership

1. Configure self-service password reset functionality

1. Validate self-service password reset functionality


#### Task 1: Create a new Azure AD tenant

1. From the lab virtual machine, start Microsoft Edge, browse to the Azure portal at [**http://portal.azure.com**](http://portal.azure.com) and sign in by using a Microsoft account that has the Owner role in the Azure subscription you intend to use in this lab.

1. In the Azure portal, navigate to the **New** blade. 

1. From the **New** blade, search Azure Marketplace for **Azure Active Directory**.

1. Use the list of search results to navigate to the **Create directory** blade.

1. From the **Create directory** blade, create a new Azure AD tenant with the following settings: 

  - Organization name: **AdatumLab100-5b**

  - Initial domain name: a unique name consisting of a combination of letters and digits. 

  - Country or region: **United States**

   > **Note**: Take a note of the initial domain name. You will need it later in this lab. 


#### Task 2: Activate Azure AD Premium v2 trial

1. In the Azure portal, set the **Directory + subscription** filter to the newly created Azure AD tenant.

   > **Note**: The **Directory + subscription** filter appears to the right of the Cloud Shell icon in the toolbar of the Azure portal 

   > **Note**: You might need to refresh the browser window if the **AdatumLab100-5b** entry does not appear in the **Directory + subscription** filter list.

1. In the Azure portal, navigate to the **AdatumLab100-5b - Overview** blade.

1. From the **AdatumLab100-5b - Overview** blade, navigate to the **Licenses - Overview** blade.

1. From the **Licenses - Overview** blade, navigate to the **Products** blade. 

1. From the **Products** blade, navigate to the **Activate** blade and activate **Azure AD Premium P2** free trial.


#### Task 3: Create and configure Azure AD users

1. In the Azure portal, navigate to the **Users - All users** blade of the AdatumLab100-5b Azure AD tenant.

1. From the **Users - All users** blade, create a new user with the following settings:

    - Name: **aaduser1**

    - User name: **aaduser1@&lt;DNS-domain-name&gt;.onmicrosoft.com** where &lt;DNS-domain-name&gt; represents the initial domain name you specified in the first task of this exercise. 

   > **Note**: Take a note of this user name. You will need it later in this lab.

    - Profile: 

        - Department: **Sales**

    - Properties: **Default**

    - Groups: **0 groups selected**

    - Directory role: **User**

    - Password: select the checkbox **Show Password** and note the string appearing in the **Password** text box. You will need it later in this lab.

1. From the **Users - All users** blade, create a new user with the following settings:

    - Name: **aaduser2**

    - User name: **aaduser2@&lt;DNS-domain-name&gt;.onmicrosoft.com** where &lt;DNS-domain-name&gt; represents the initial domain name you specified in the first task of this exercise. 

   > **Note**: Take a note of this user name. You will need it later in this lab.

    - Profile: 

        - Department: **Finance**

    - Properties: **Default**

    - Groups: **0 groups selected**

    - Directory role: **User**

    - Password: select the checkbox **Show Password** and note the string appearing in the **Password** text box. You will need it later in this lab.


#### Task 4: Assign Azure AD Premium v2 licenses to Azure AD users

   > **Note**: In order to assign Azure AD Premium v2 licenses to Azure AD users, you first have to set their location attribute.

1. From the **Users - All users** blade, navigate to the **aaduser1 - Profile** blade and set the **Usage location** to **United States**.

1. From the **aaduser1 - Profile** blade, navigate to the **aaduser1 - Licenses** blade and assign to the user an Azure Active Directory Premium P2 license with all licensing options enabled.

1. Return to the **Users - All users** blade, navigate to the **aaduser2 - Profile** blade, and set the **Usage location** to **United States**.

1. From the **aaduser2 - Profile** blade, navigate to the **aaduser2 - Licenses** blade and assign to the user an Azure Active Directory Premium P2 license with all licensing options enabled.

1. Return to the **Users - All users** blade, navigate to the Profile entry of your user account and set the **Usage location** to **United States**.

1. Navigate to **Licenses** blade of your user account and assign to it an Azure Active Directory Premium P2 license with all licensing options enabled.

1. Sign out from the portal and sign back in using the same account you are using for this lab. 

   > **Note**: This step is necessary in order for the license assignment to take effect. 


#### Task 5: Manage Azure AD group membership

1. In the Azure portal, navigate to the **Groups - All groups** blade. 

1. From the **Groups - All groups** blade, navigate to the **Group** blade and create a new group with the following settings:

    - Group type: **Security**

    - Group name: **Sales**

    - Group description: **All users in the Sales department**

    - Membership type: **Dynamic User**

    - Dynamic user members: 

        - Simple rule

        - Add users where: **department Equals Sales**

1. From the **Groups - All groups** blade, navigate to the **Group** blade and create a new group with the following settings:

    - Group type: **Security**

    - Group name: **Sales and Finance**

    - Group description: **All users in the Sales and Finance departments**

    - Membership type: **Dynamic User**

    - Dynamic user members: 

        - Advanced rule: **(user.department -eq "Sales") -or (user.department -eq "Finance")**

1. From the **Groups - All groups** blade, navigate to the blades of **Sales** and **Sales and Finance** groups, and note that the group membership evaluation is in progress. Wait until the evalution completes, then navigate to the **Members** blade, and verify that the group membership is correct.


#### Task 6: Configure self-service password reset functionality

1. In the Azure portal, navigate to the **AdatumLab100-5b - Overview** blade. 

1. From the **AdatumLab100-5b - Overview** blade, navigate to the **Password reset - Properties** blade. 

1. On the **Password reset - Properties** blade, configure the following settings:

    - Self service password reset enabled: **Selected**

    - Selected group: **Sales**

1. From the **Password reset - Properties** blade, navigate to the **Password reset - Auhentication methods** blade and configure the following settings:

    - Number of methods required to reset: **1**

    - Methods available to users: 

        - **Email**

        - **Mobile phone**

        - **Office phone**

        - **Security questions**

        - Number of security questions required to register: **3**

        - Number of security questions required to reset: **3**

        - Select security questions: select **Predefined** and add any combination of 5 predefined security questions

1. From the **Password reset - Authentication methods** blade, navigate to the **Password reset - Registration** blade, and ensure that the following settings are configured:

    - Require users to register when signing in?: **Yes**

    - Number of days before users are asked to re-confirm their authentication information: **180**


#### Task 7: Validate self-service password reset functionality

1. Open an InPrivate Microsoft Edge window.

1. In the new browser window, navigate to the Azure portal and sign in using the **aaduser1** user account. When prompted, change the password to a new value.

   > **Note**: You will need to provide a fully qualified name of the **aaduser1** user account, including the Azure AD tenant DNS domain name, as noted earlier in this lab.

1. When prompted with the **More information required** message, continue to the **don't lose access to your account** page.

1. On the **don't lose access to your account** page, note that you need to set up at least one of the following options:

    - **Office phone**

    - **Authentication Phone**

    - **Authentication Email**

    - **Security Questions**

1. From the **don't lose access to your account** page, configure answers to 5 security questions you selected in the previous task

1. Verify that you successfully signed in to the Azure portal.

1. Sign out as **aaduser1** and close the InPrivate browser window.

1. Open an InPrivate Microsoft Edge window.

1. In the new browser window, navigate to the Azure portal and, on the **Pick an account** page, type in the **aaduser1** user account name. 

1. On the **Enter password** page, click the **Forgot my password** link.

1. On the **Get back into your account** page, verify the **User ID**, enter the characters in the picture or the words in the audio, and proceed to the next page.

1. On the next page, provide answers to thre security questions using answers you specified in the previous task.

1. On the next page, enter twice a new password and complete the password reset process.

1. Verify that you can sign in to the Azure portal by using the newly reset password. 

> **Result**: After you completed this exercise, you have created a new Azure AD tenant, activated Azure AD Premium v2 trial, created and configured Azure AD users, assigned Azure AD Premium v2 licenses to Azure AD users, managed Azure AD group membership, as well as configured and validated self-service password reset functionality


### Exercise 2: Manage Azure AD-integrated SaaS applications

The main tasks for this exercise are as follows:

1. Add an application from the Azure AD gallery

1. Configure the application for a single sign-on

1. Assign users to the application

1. Validate single sign-on for the application


#### Task 1: Add an application from the Azure AD gallery

1. In the Azure portal, navigate to the **AdatumLab100-5b - Overview** blade. 

1. From the **AdatumLab100-5b - Overview** blade, navigate to the **Enterprise applications - All applications** blade.

1. From the **Enterprise applications - All applications** blade, navigate to the **Add an application** blade. 

1. On the **Add an application** blade, search the application gallery for the **Microsoft OneDrive**. 

1. Use the list of search results to navigate to the **Microsoft OneDrive** add app blade and add the app.


#### Task 2: Configure the application for a single sign-on

1. From the **Microsoft OneDrive - Overview** blade, navigate to the **Microsoft OneDrive - Getting started** blade. 

1. On the **Microsoft OneDrive - Getting started** blade, use the **Configure single sign-on (required)** option to navigate to the **Microsoft OneDrive - Single sign-on** blade. 

1. On the **Microsoft OneDrive - Single sign-on** blade, select the **Password-based** option and save the configuration.


#### Task 3: Assign users to the application

1. Navigate back to the **Microsoft OneDrive - Getting started** blade. 

1. On the **Microsoft OneDrive - Getting started** blade, use the **Assign a user for testing (required)** option to navigate to the **Users and groups** blade for **Microsoft OneDrive**. 

1. From the **Users and groups** blade for **Microsoft OneDrive**, navigate to the **Add Assignment** blade and add the following assignment:

    - Users and groups: **Sales and Finance**

    - Select role: **Default access**

    - Assign Credentials: 

        - Assign credentials to be shared among all group members: **Yes**

        - Email Address: the name of the Microsoft Account you are using for this lab

        - Password: the password of the Microsoft Account you are using for this lab

1. Sign out from the Azure portal and close the Microsoft Edge window.


#### Task 4: Validate single sign-on for the application

1. Open a Microsoft Edge window.

1. In the Microsoft Edge window, navigate to the Application Access Panel at [**http://myapps.microsoft.com**](http://myapps.microsoft.com) and sign in by using the **aaduser2** user account. When prompted, change the password to a new value.

   > **Note**: You will need to provide a fully qualified name of the **aaduser2** user account, including the Azure AD tenant DNS domain name, as noted earlier in this lab.

1. On the Access Panel Applications page, click the **Microsoft OneDrive** icon.

1. When prompted, add the My Apps Secure Sign-in Extension and enable it, including the **Allow for InPrivate browsing** option.

1. Navigate again to the Application Access Panel at [**http://myapps.microsoft.com**](http://myapps.microsoft.com) and sign in by using the **aaduser2** user account. 

1. On the Access Panel Applications page, click the **Microsoft OneDrive** icon.

1. Verify that you have successfully accessed the Microsoft OneDrive application without having to re-authenticate.

1. Sign out from the Application Access Panel and close the Microsoft Edge window.

   > **Note**: Make sure to launch Microsoft Edge again, browse to the Azure portal, sign in by using the Microsoft account that has the Owner role in the Azure subscription you were using in this lab, and use the **Directory + subscription** filter to switch to your default Azure AD tenant once you complete this lab.

> **Result**: After you completed this exercise, you have added an application from the Azure AD gallery, configured the application for a single sign-on, assigned users to the application, and validated single sign-on for the application.
