# SAML Lab Part 2 - Enable Okta for MFA

Okta and most other IdPs support Second Factor Authentication (2FA) or Multi-Factor Authentication (MFA). MFA is becoming more and more common in our customers because it is more secure than a Single Factor. In this part of the lab you will enable MFA for your SAML users. The configuration is all in Okta - Tableau does not really know that MFA is enabled. All Tableau needs to do is present any web pages that the MFA flow renders in web pages.

## Step 1 - Configure MFA

Sign back into Okta using the Okta Administrator account. From the **Security** menu select **Multifactor**

![Okta - Multifactor Menu](images/2018-12-27-13-43-24.png)

Okta supports several factor types and you can activate multiple types at the same time. SMS Authentication is one of the simpler to set up if you have a phone that can receive SMS messages. Enable SMS Authentication if you think you can receive SMS messages during the Lab session or you want to test this later

![Okta - Enable Factor Types](images/2018-12-27-13-48-59.png)

You can also create a security question. Enable this factor in addition to SMS. You will configure Okta to allow you to choose which factor to use on login.

Select Activate on the drop down after clicking on the factor you want to enable:

![Okta - Activate Factor Type](images/2018-12-27-13-53-03.png)

Okta is very flexible in how you enable MFA for groups or users. Some IdPs allow the user to self register for MFA. In this Lab we will force all users of Tableau Online to use one of the activated Multi Factor Types when authenticating.

In the Tableau Online Application scroll to the bottom where the Sign On Policy is located:

![Okta Sign On Policy](images/2018-12-27-13-57-51.png)

Click **Add Rule** and give it a name. Read the settings and understand the options. You can leave most options as defaults to enable MFA for all users assigned to the app.

> ![Note](images/icon-note.png) You can limit the rule to a subset of user or groups and to certain network zones. You can also limit the rule to certain platforms.

![Okta - Sign on Rule Top](images/2018-12-27-14-06-55.png)

The rules pop up has more sections. Scroll down to see the Device Trust and Actions Sections:

![Okta - Device Trust and Actions](images/2018-12-27-14-08-18.png)

We did not configure device trust so Any is the only option.

For **Actions** select the *Prompt for Factor* checkbox. We already activated some Factor Types so all we need to do is to configure how often we want to prompt. Select *Every sign on* then ![Okta - Save](images/icon-save-small.png)

![Okta - Every sign on](images/2018-12-27-14-12-34.png)

The Sign On Policy should look like this:

![Okta - Finished Sign On Policy](images/2018-12-27-14-13-59.png)

Sign out of Okta and Tableau Online and Sign onto Online again using the Online user we set up for SAML.

![Tableau Online - Sign In](images/2018-12-27-14-17-38.png)

You will be redirected to Okta:

![Okta - Sign In](images/2018-12-27-14-19-31.png)

After entering the usual username and password you should get a second factor prompt. You can choose which factor to use by clicking on the down arrow next to the shield:

![Okta - Select an authentication factor](images/2018-12-27-14-25-33.png)

Pick *SMS authentication* if you can receive Text Messages, or *Security Question* if you do not have your phone  

> ![Note](images/icon-note.png) If this is the first time for SMS you may be prompted to enter phone information:

Here is how SMS Authentication looks:

![Okta - SMS MFA](images/2018-12-27-14-27-49.png)

In the Apple Messages app:

![IOS - SMS MFA](images/2018-12-27-14-50-22.png)

If you select Security Question you should be prompted to answer your question:

![Okta - Security Question](images/2019-01-03-21-32-07.png)

Enter your answer anc click **Verify**