## lAZy Changelog:

##  3/22: Azure Administrator v1.0.1.0 released


## 4/12/22: lAZy v1.0.2.0 released
* Added Intune functionality
* Updated password generator so that passwords are easier to read
* Removed the glaring _What's This_? button on Get Client form, replaced with ToolTip
* Moved all administrative functions to install stage (module installs, folder creation, etc.)
  * Previously, most of this was done on first run. If not running as an admin, it wouldn't work
* Enhanced action validation by implementing pop-ups when an error is encountered. Logging has not changed except that each module has its own log folder now.
* Updated input validation for User Email fields in Azure modules. Whereas previously it would check for a domain with .com, .edu, or .gov, the app will now check the entered name against lAZy user's
tenant and only unlock the action buttons if the entered email address exists. A ToolTip has been added that will appear when hovering over the User Email field when the entered email
does not exist
