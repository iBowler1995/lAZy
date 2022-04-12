# Welcome to the lAZy (formerly known as Lazy Azure Administrator) Project!

Azure Administrator (AA) is a simple GUI application designed to handle most of your help desk needs. It currently focuses on user and group management, but future updates I plan to bring will add even more features such as mailbox management and AAD/Intune device management!

# How to Install
lAZy is lightweight and extremely simple to install. Launch the MSI manually and click through the setup wizard, or install it programatically using the following command:
`msiexec /i lAZy.msi /qn`

# Environment deployment pre-requisite(s)
Currently the only pre-requisite to deploying lAZy to your environment is you'll need to set up a registered application in your AAD tenant. Microsoft has a really easy and straightforward guide on this: https://docs.microsoft.com/en-us/graph/auth-v2-user as well as this article on how to set up delegated API permissions: https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-configure-app-access-web-apis NOTE: The redirect I use for lAZy in my environment: https://login.microsoftonline.com/common/oauth2/nativeclient
Once you have your application set up, note your ApplicationID (also called ClientID) and enter it in on first run.

# First Run
All modules will be locked until you Log In. On first run, clicking the Log In button will open the GetClient form for the user to paste the ClientID into (Author's note: While I wouldn't share your application's ID with the world, it doesn't necessarily need to be kept in a top-secret vault. As long as you have the *Who can use this application or access this API?* setting for your registered application set to *Accounts in this organizational directory only*, only accounts from your tenant can authenticate to the app or API.)
Once you've successfully authenticated to your AAD tenant, the other modules will be unlocked. Do note that if MFA is enabled on your account, you'll need to approve the login request.

# Module Functionality
* Assign License: Accepts user's email as input and assigned checked licenses to the user. (BUG NOTE: Currently when trying to assign multiple licenes at once, the task may fail due to Graph API limiting. Currently investigating.)
* Add User to Group: On form load, gets all groups in your organization. Accepts user's email as input and add's user to any of the selected groups (can use ctrl click to select multiple groups)
* Create Assigned Group: Accepts incipient group's displayName (required), mail nickname (required; no spaces is best, but use %20 for space if needed). Based on what options are checked, can create one of three types of groups: 1. a standard, statically assigned security group. Mail not enabled, because not an M365 group. 2. M365 group, mail disabled, or 3. M365 group, mail enabled
* Create New User: Simple to fill out form to input incipient user's information on. Only requires first and last name to create the account. Allows for assignment of licenses (subject to the same bug mentioned above) and assignment to group(s). Random 12-character password will be generated and copied to your clipboard
* Disable User: Accepts user's email address and disables user
* Edit User: Currently able to edit 7 fields for user: Given name, surname, title, office, manager email, moible phone, and department
* Enable User: Accepts user's email address and enables user
* Remove from Group: Accepts user's email as input, loads user's groups, and removes user from any selected groups
* Reset Password: Accepts user's email address as input, as well as new password (if you're not using the Random buttonthat is, which is generally more secure than most help desk assigned passwords I've run into in my times)
* Terminate User: Accepts user's email address as input and terminates user. Following actions are taken: 1. User disabled 2. Z_Term_ added to the front of the user's display name. 3. Removes user from all static groups (cannot remove from dynamic groups). 4. Removes all assigned licenses to the user. (Author's note: As I introduce mailbox management, I plan on adding an optional parameter to let you convert user boxes to shared mailboxes for termed users.)
* Application Install Status: Review or export the install status of a managed app on Intune devices
* Assign Application: assign an Intune application to a specified AAD group with specifed install intent
* Compliance Policies: Review or export policy status on Intune devices as well as assign policies to specified AAD group(s)
* Configuration Policies: Review or export policy status on Intune devices as well as assign policies to specified AAD group(s)
* Device Last Logged On User: Retrieve the user who last logged into the specified Intune device
* Rename Device: Allows for renaming of Intune devices singularly or all at once
* Reboot Device: Reboots specified Intune device
* Reset Device: Reset Intune device with the chosen options
* Sync Device: Sync Intune device singularly or all at once (not available in Intune portal GUI)
* Windows Update Status: Review or export Windows Update status for a chosen Intune Update Ring or a specified device (the update ring the specified device is a part of must also be selected for this feature to work)

# Functionality Notes
* All Azure forms requiring user email address for input will have the action button disabled until the email address field contains an email that is registered with the current user's domain.
* All Intune forms requiring some sort of selection will have the action button disabled until the selection(s) have been made.
* Microsoft license options available in lAZy can be expanded; I have selected the most used (in my experience) to start with, but if you have other licenses you'd like to see, please submit a feature request *along with the license SkuID.* The SkuID can be found in several ways, including querying with Graph: `GET https://graph.microsoft.com/v1.0/subscrikedSkus`, or with the Microsoft.Graph.Identity.DirectoryManagement module command `Get-MgSubscribedSku | select skuPartNumber, SkuId | Format-List`

# Required delegated Graph API permissions
Note: only one is required from each list. Each list is also sorted from least to most privileged permissions for better clarity. See https://docs.microsoft.com/en-us/graph/permissions-reference for more/better information on Graph API permissions
* Assigning licenses: User.ReadWrite.All, Directory.ReadWrite.All
* Adding user to group(s): GroupMember.ReadWrite.All, Group.ReadWrite.All, Directory.ReadWrite.All, Directory.AccessAsUser.All
* Creating assigned groups: Group.ReadWrite.All, Directory.ReadWrite.All, Directory.AccessAsUser.All
* Creating new user: 	User.ReadWrite.All, Directory.ReadWrite.All, Directory.AccessAsUser.All
* Disable user, Edit user, Enable user, Reset password:: User.ReadWrite, User.ReadWrite.All, User.ManageIdentities.All, Directory.ReadWrite.All, Directory.AccessAsUser.All
* Remove from group: GroupMember.ReadWrite.All, Group.ReadWrite.All, Directory.ReadWrite.All, Directory.AccessAsUser.All
* Terminate user: each of the above 
* Assign App/Install status: DeviceManagementApps.ReadWrite.All
* Compliance Policy Assign/status: DeviceManagementConfiguration.ReadWrite.All
* Configuration Policy Assign/status: DeviceManagementConfiguration.ReadWrite.All
* Last logged on user: DeviceManagementManagedDevices.ReadWrite.All
* Rename device: DeviceManagementManagedDevices.PriviligedOperation.All
* Reboot device: DeviceManagementManagedDevices.PriviligedOperation.All
* Reset device: DeviceManagementManagedDevices.PriviligedOperation.All
* Sync device: DeviceManagementManagedDevices.PriviligedOperation.All
* Update status:  DeviceManagementConfiguration.ReadWrite.All
