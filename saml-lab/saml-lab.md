# SAML Lab - Setup Instructions

This lab assumes you have a Tableau Online Site and an Okta Development Account. If you have already configured your site for SAML you may want to save your existing configuration and create a new configuration for the lab as we will use Okta to configure SCIM and MFA.

## Step 1 - Sign into Online and Enable SAML  

In your Web Browser Log into you Online site as a Site Administrator and Select the **Authentication** section from the **Settings** menu.

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

![Okta - Sign On](images/2018-12-26-15-37-19.png)

You can now add the *ACS URL* and *Tableau Server entity ID* from your Online site. Note that Okta does not read the Metadata file but uses the second option in Step 1.  

You can click on the **View Setup Instructions** on the Okta page. This link is specific to your Site as it includes the link to the Idp Metadata. The setup instructions tell you to the following:

Copy the Entity ID and ACS from Tableau to Okta:

![Tableau Online - Entity ID and ACS](images/2018-12-26-15-48-42.png)

![Okta - Entity ID and ACS](images/2018-12-26-15-49-07.png)

Note that the Form fields may be in a different order between the app. This is why exchanging metadata via the metadata files is usually the safest option if it is available.

Note also that we do not need to download the Tableau certificate and load it into Okta. Why not?

Next download the Idp Metadata by clicking on the *Identity Provider metadata* link and saving the XML (right-click > Save as... in Chrome):

![Okta - IdP Metadata](images/2018-12-26-15-59-58.png)

or right-click on the link and select *Save link as...*

![Okta - IdP Metadata - Save Link as...](images/2018-12-26-16-01-53.png)

Whichever way you choose, save the file to your local computer (I usually make the filename more explicit than the default)

![Okta - IdP Metadata - Save Link as... - Explorer ](images/2018-12-26-16-04-12.png)

Back in Tableau Online go to *Step 4* and Browse to the IdP metadata file you just downloaded:

![Tableau Online - Import Idp Metadata](images/2018-12-26-16-06-27.png)
