# Reset Device module

## How to use:
* Select the desired device from the list up top **_or_** enter the device name under the list
* Choose reset option
  * Wipe: restore device to OOBE
    * When this option is chosen (and only when this option is chosen), the 'Keep User Data' checkbox is unlocked. Use this checkbox if you wish to keep the user account and profile on the device
  * Retire: 
    * Managed apps are uninstalled (Win32 apps will **_not_** be uninstalled, users must do this) 
    * configurations are no longer enforce and users can change settings
    * All Wi-Fi and VPN profile settings are removed
    * All certificate profile settings are removed
    * Removes email that’s EFS-enabled. This includes emails and attachments in the Mail app for Windows. Removes mail accounts that were provisioned by Intune. (PST or OST files are not removed!)
    * All AAD user accounts will be removed (__Warning:__ there will be no ability to sign in afterwards if a local user is not set up first)
    * User personal data is **_not_** removed
    * Removes device from Intune at next device check-in
    * Unjoins from AAD
  * Autopilot reset: 
    * Wipes all MDM Policies and User data. Resets user settings back to default
    * Removes user-installed apps, Keeps user accounts
    * Resets the operating system to its default state and management settings. Keeps AAD join
