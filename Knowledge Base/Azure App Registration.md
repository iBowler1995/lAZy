# How to set up an Azure App registration and apply the appropriate API permissions to use lAZy

## Step 1: Register your app:
1. Sign into The Azure portal
2. In the left-hand pane, select the Azure Active Directory service, then select App registrations > New registration
3. When the creation page appears, enter your application's registered information:
  * Name: a meaningful name that will be displayed to users of the app (not very relevant in the case of lAZy as we only need the ClientID)
  * Supported account type:
    * Accounts in this organizational directory only (single tenant only): All users and guest accounts in your directory can use your application or API. Use if app will be internal only
    * Accounts in any organizational structure: All users with a work or school account from Microsoft can use your application or API. This includes schools and businesses that use Office 365.
      * Use this option if
