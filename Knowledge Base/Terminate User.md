# Terminate User module

## Description: Terminates a user, taking the following actions:
* Disables User
* Adds Z_Term_ in front of user's display name
* Removes users from all static groups (cannot remove from dynamic groups)
* Removes all assigned licenses to the user

## How to use:
* Enter email address of user to terminate
  * Terminate button will be disabled until User Email field has a valid email registered to the currently authenticated tenant (tl;dr: field must have a real user email in it)
