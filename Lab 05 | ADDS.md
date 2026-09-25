# Lab 05 | ADDS
## OU Creation
OUs are how objects are stored on the AD environment
  * Tools > ADU&C
  * Right click on the domain
  * New > OU
  * Name it SYS255
  * Create 3 sub-OUs named Accounts, Computers, and Groups
## Adding Users and Groups
  * Add 3 new users to the Accounts OU
    * Alice, Bob, Charlie
  * Move WKS01 from the domain default Computers folder to SYS255/Computers
  * Create a security group within SYS255/Groups and call it custom-desktop
    * Alice and Bob should be members<br>

**BEST PRACTICE FOR GROUPS: Many times, organizations will have a number of groups defined in their AD domain. For this reason, it is a best practice to have a naming convention that purposefully describes what the groups do. A lot of times, groups allow or disallow users permission to folders and resources on the network. For this reason, a commonly found group membership is in the form of something like this: DepartmentName_RW_ACL or GP_WindowsIESettings_ACL. This gives administrators an idea of what the group is for, and who may need to be a member.**

## Group Policy - User
Using group policy we can manage multiple users at once.  
  * Tools > GPM
  * Right click SYS255 and create a new GPO
    * Call it sys255-desktop
  * Add custom-desktop to the security filtering section
  * Remove authenticated users
  * Add Domain Computers to the security filter
  * Delegation tab -> Advanced (Uncheck Apply Group Policy, Select Deny for Domain Computers)
  * Right click sys255-desktop > Edit
### Removing the Recycle Bin
  * User Config > Policies > Admin > Desktop
  * Find "remove recycle bin icon from desktop" setting
  * Set it to enable

## Group Policy - Computer
  * Create a new link to a GPO under SYS255/Computers called DisableLastLogin
  * Add Domain Computers and remove auth users from security filter
  * Edit > Computer Config > Policies > Windows > Security Settings > Local Policies > Security Options
  * Enable "Interactive logon: Don't display last signed-in"
