# SAML Lab - Setup Instructions

This lab assumes you have a Tableau Online Site and an Okta Development Account. If you have already configured your site for SAML you may want to save your existing configuration and create a new configuration for the lab as we will use Okta to configure SCIM and MFA.

## Step 1 - Sign into Online and Enable SAML  

In your Web Browser Log into your Online site as a Site Administrator and Select the **Authentication** section from the **Settings** menu.

Check *enable an additional authentication option* under **Authentication types**

![Tableau Online authentication settings](images/2018-12-26-15-13-58.png)

## Step 2 - Sign into the Okta Development Console and create a new application

You may need to switch from the **Developer Console** to the **Classic UI**. The Developer console looks like this after clicking **Add Application** You can do that from the top right corner

![Okta Developer Console - Add Application](images/2018-12-26-15-12-10.png)

The Classic UI looks like this:

![Okta Classic UI - Add Application](images/2018-12-26-15-22-45.png)

Search for Tableau and Select Tableau Online:

![Okta - Tableau Online Search](images/2018-12-26-15-24-03.png)

You can change the Application Label and change the application visibility. For the lab you can leave the defaults. Click **Done** to continue

![Okta - Add Tableau Online](images/2018-12-26-15-27-19.png)

The **Assignments** tab will display next. You can add users here but we are going to enable automatic provisioning with SCIM so we will add users later. If you do not want to enable SCIm you can add users and/or groups on this tab.

![Okta - Assignments](images/2018-12-26-15-34-15.png)

For now select the **Sign On** tab and then the **edit** button:

## Step 3 - Configure the Okta Sign On details and Import IdP Metadata to Tableau Online

![Okta - Sign On](images/2018-12-26-15-37-19.png)

You can now add the *ACS URL* and *Tableau Server entity ID* from your Online site. Note that Okta does not read the Metadata file but uses the second option in Step 1.  

You can click on the **View Setup Instructions** on the Okta page. This link is specific to your Site as it includes the link to the Idp Metadata. The setup instructions tell you to the following:

Copy the Entity ID and ACS from Tableau to Okta:

![Tableau Online - Entity ID and ACS](images/2018-12-26-15-48-42.png)

![Okta - Entity ID and ACS](images/2018-12-26-15-49-07.png)

> ![Warning](images/icon-warning.png) The Form fields may be in a different order between the app. This is why exchanging metadata via the metadata files is usually the safest option if it is available.
> Take care to copy the fields correctly. The Entity ID looks like a URL but has the word _metadata_ it it. The ACS URL is a real URL and has _SSO_ in it.

> ![Note](images/icon-note.png) Technically the Entity ID is a just a string identifier

> ![Note](images/icon-note.png) We do not need to download the Tableau certificate and load it into Okta. Why not?

Next download the Idp Metadata by clicking on the *Identity Provider metadata* link and saving the XML (right-click > Save as... in Chrome):

![Okta - IdP Metadata](images/2018-12-26-15-59-58.png)

or right-click on the link and select *Save link as...*

![Okta - IdP Metadata - Save Link as...](images/2018-12-26-16-01-53.png)

Whichever way you choose, save the file to your local computer (I usually make the filename more explicit than the default)

![Okta - IdP Metadata - Save Link as... - Explorer ](images/2018-12-26-16-04-12.png)

Back in Tableau Online go to *Step 4* and Browse to the IdP metadata file you just downloaded:

![Tableau Online - Import Idp Metadata](images/2018-12-26-16-06-27.png)

## Step 4 - Configure Okta Provisioning

Tableau Online now supports automatic user provisioning from Okta using an open standard called [System for Cross-domain Identity management (SCIM)](http://www.simplecloud.info/)

Configuring SCIM requires some setup in Tableau Online and Okta.

In Tableau Online you enable SCIM at the bottom of the Authentication Setup page:

![Tableau Online - Enable SCIM](images/2018-12-26-18-09-56.png)

In Okta you select the Provisioning Tab in the Applications menu:

![Okta - Provisioning](images/2018-12-26-18-06-02.png)

Click on **Configure API Integration** then check *Enable API integration* and copy the *Base URL* and *API Token* from the Online setup page.

![Okta - Enable SCIM](images/2018-12-26-18-08-31.png)

Note that the Secret API Token will not show again and if you forget it you will need to generate a new one to configure Okta.

You can click **Test API Credentials** to make sure you copied the Base URL and Secret correctly. Click **Save** when done.

## Step 5 - Add a User to Okta

Now that Okta and Tableau Online are configured you can add a new user to Okta and test the SCIM provisioning (and de-provisioning). Most Tableau customers will link Okta to an external Directory or Identity Store like Active Directory or LDAP. Also, most customers will manage users via groups but in this lab you can create a single user directly in Okta then assign the user to our Tableau Online application.

In the **Directory** menu select **People** then **Add Person**

![Okta - Add Person](images/2018-12-26-18-32-21.png)

Enter the details of a new Okta user. Note that this user can be assigned to multiple applications in Okta and that is an extra step below.

![Okta - Add Person details](images/2018-12-26-18-42-02.png)

Click **Save**

## Step 6 - Assign the user to the Tableau Online application

You can assign users to applications in several ways. You can either do it from the Directory by clicking the user then **Assign Applications**

![Okta - User Assign 1](images/2018-12-26-18-45-22.png) and then selecting one or more applications:

![Okta - User Assign 2](images/2018-12-26-18-47-03.png)

Leave the username as the email and click **Save and Go Back**

![Okta - Save User Assignment](images/2018-12-26-18-49-04.png)

Alternatively you can select **Applications** then the Tableau Online Application. Now you can assign the new user to Tableau Online. Click on **Assignments** in the Applications menu in Okta. Click on **Assign** then *Assign to People*

![Okta - Assign Users 3](images/2018-12-26-18-50-50.png)

With SCIM enabled this is all you need to do. Okta will provision the new user in Tableau. You can confirm this by going back to Tableau Online and checking to see if the user got added:

![Tableau Online - Users](images/2018-12-26-18-52-57.png)

[Note that the user was added as a Viewer - I am not sure if the default site role can be configured. Try testing with groups?]

## Step 7 - Test SAML Login

Sign out of your Site Admin account in Tableau Online and also sign out of the Okta Developer Console. If you do not sign out of Okta then when you sign in to Tableau using the new account Okta might show and error or send back the wrong assertion.

Now Sign into Tableau Online using the username of the user you assigned to the Tableau Online application in Okta. The browser should redirect you to Okta and present a login form.

## Step 8 (Optional) - Configure MFA

Okta and most other IdPs support Second Factor Authentication (2FA) or Multi-Factor Authentication (MFA). MFA is becoming more and more common in our customers because it is more secure than a Single Factor. In this part of the lab you will enable MFA for your SAML users. The configuration is all in Okta - Tableau does not really know that MFA is enabled. All Tableau needs to do is present any web pages that the MFA flow renders in web pages.

To configure Okta for MFA:

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

Click **Add Rule** and give it a name. Read the settings and understand the options. You can leave most options as defaults to enable MFA for all users assigned to the app. Note you can limit the rule to a subset of user or groups and to certain network zones. You can also limit the rule to certain platforms.

![Okta - Sign on Rule Top](images/2018-12-27-14-06-55.png)

The rules pop up has more sections. Scroll down to see the Device Trust and Actions Sections:

![Okta - Device Trust and Actions](images/2018-12-27-14-08-18.png)

We did not configure device trust so Any is the only option.

For **Actions** select the *Prompt for Factor* checkbox. We already activated some Factor Types so all we need to do is to configure how often we want to prompt. Select *Every sign on* then **Save**

![Okta - Every sign on](images/2018-12-27-14-12-34.png)

The Sign On Policy should look like this:

![Okta - Finished Sign On Policy](images/2018-12-27-14-13-59.png)

Sign out of Okta and Tableau Online and Sign onto Online again using the Online user we set up for SAML.

![Tableau Online - Sign In](images/2018-12-27-14-17-38.png)

You will be redirected to Okta:

![Okta - Sign In](images/2018-12-27-14-19-31.png)

After entering the usual username and password you should get a second factor prompt. You can choose which factor to use by clicking on the down arrow next to the shield:

![Okta - Select an authentication factor](images/2018-12-27-14-25-33.png)

Pick *SMS authentication* if you can receive Text Messages or *Security Question*

Here is how SMS Authentication looks. Note that the users phone has already been registered. If this is the first time for SMS you m ay be prompted to enter phone information:

![Okta - SMS MFA](images/2018-12-27-14-27-49.png)

In the Apple Messages app:

![IOS - SMS MFA](images/2018-12-27-14-50-22.png)