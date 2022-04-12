# How to set up an Azure App registration and apply the appropriate API permissions to use lAZy

## Step 1: Register your app:
1. Sign into The Azure portal
2. In the left-hand pane, select the Azure Active Directory service, then select App registrations > New registration
3. When the creation page appears, enter your application's registered information:
  * Name: a meaningful name that will be displayed to users of the app (not very relevant in the case of lAZy as we only need the ClientID)
  * Supported account type:
    * Accounts in this organizational directory only (single tenant only): All users and guest accounts in your directory can use your application or API.
      * Use this option if your target audience is internal only
    * Accounts in any organizational structure: All users with a work or school account from Microsoft can use your application or API. This includes schools and businesses that use Office 365.
      * Use this option if your target audience is business or education customers and to enable multitenancy (this is a good option for MSPs or users with multiple tenants)
    * Accounts in any organizational directory and personal Microsoft accounts: All users with a work or school, or personal Microsoft account can use your application or API. It includes schools and businesses that use Office 365 as well as personal accounts that are used to sign in to services like Xbox and Skype.
      * Use this option to target the widest set of Microsoft identities and to enable multitenancy (I recommend against this, as most personal Microsoft accounts don't even necessarily have the ability to access Intune/Azure)
  * Redirect URI: For lAZy, set the Mobile and Desktop applications redirect URI to `https://login.microsoftonline.com/common/oauth2/nativeclient`
4. Click Register
5. Take note of the application (client) ID. This will be needed the first time you run lAZy (or if you need to change tenants)

## Step 2: Configure API permissions: 
1. Open the app you just registered
2. In the left-hand pane, select API permissions
  * There are two options when applying API permissions: application and delegated
    * Application permission: these permissions are for automation purposes, and shouldn't be used for lAZy. If, however, you choose to use the PowerShell functions I've published utilizing the Graph API, you'll want to use these if you intent to automate them.
    * Delegated (what lAZy needs): Allows the application to access the API on behalf of whichever user is authenticated (which means actions can be tracked by your organization)
3. Use [this document](https://github.com/iBowler1995/LazyAzureAdministrator/blob/main/Knowledge%20Base/API%20Permissions.md) to configure appropriate API permissions for lAZy
4. Once all permissions are applied, hit the checkmark that syas "Grant admin consent for [organization]," or else users won't be able to access AAD/Intune
