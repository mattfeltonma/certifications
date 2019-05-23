# Configure MFA Settings

## General
* Available via Azure AD Premium, MFA for Office 365, and for Azure AD Global Administrators
* Users who are enforced for MFA overrides any Conditional Access policies enforcing it
* Require MFA by enforcing it on a user, configuring conditional access, or requiring it based upon sign on risk using Identity Protection
* When user is enabled for MFA, non-browser apps are unaffected and apps using modern authentication will work as long as the existing access token is valid
* Activity Report in MFA Blade in Azure AD is for Azure MFA Server only

## Azure MFA Services vs Azure MFA Server
* MFA Services supports SaaS apps in application gallery
* MFA Services supports web apps published through AAD Proxy
* MFA Server supports IIS Apps

## Azure MFA Authentication Factors
* Mobile App Notification
* Mobile App Verification Code
* Phone Call
* One-way SMS
* Hardware Token (OATH)

## Azure MFA Service Configuration (MFA Portal)
* Allow/Disallow Application Passwords
* Skip MFA for Trusted IPs
* Set authentication factors
* Allow users to remember MFA authentications on trusted devices for 0-60 days (def 14)
	
## Azure MFA Server Configuration
* One time bypass for a user
* SMS timeout (def 60 sec)
* Cache MFA for multiple authentications based on User, IP, or application
* Check MFA Server status

## Azure MFA Service Configuration (Azure Portal)
* Lock out a user based on the number of denied MFA requests including a reset counter and lockout duration
* Block MFA for specific users in order to lock them out for 90 days (can be manually removed from this list)
* Allow users to submit Fraud Alerts when they receive MFA requests they didn’t initiate; users can be blocked automatically; setup a code (number) users can select to report fraud via phone
* Configure OATH tokens
* For phone greetings, configure the source phone number, number of pin attempts and a custom greeting

## Azure MFA States
* Disabled
* Enabled -> User enrolled for MFA but not yet registered
* Enforced -> User enrolled for MFA and registered

## Azure MFA User Specific Options
* Force the user to provide contact methods again
* Delete all the user’s app passwords
* Restore MFA prompts for all of the users remembered devices

## Enable MFA For a User
* MFA Portal (Get there via Azure Portal)
* Enable via PowerShell with script below:
* Import-Module MSOnline
$st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
$st.RelyingParty = "*"
$st.State = "Enabled"
$sta = @($st)
Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

# Manage Microsoft Azure AD Directory Groups

## General
* Direct, Dynamic, or Synced
* Security Groups or Office 365 Groups
* All Users group is a dynamic group that contains all tenant users and guest users by default
* Office 365 Groups support blocking the usage of certain words in the names which can be uploaded via CSV
* Office 365 Groups support enforcing a naming convention which can add a prefix or suffix which is either a custom string or an attribute from the user who created it
* Office 365 Groups that are deleted by a user or automatically by an expiration policy can be restored for up to 30 days

## Dynamic Groups
* Supported for both Security Groups and Office 365 Groups
* Requires Azure AD Premium P1 be associated with the Azure AD tenant
* Created for groups that will contain either Users or Devices
* Manage membership based on the user or device attributes

## Self-Service Group Management
* Not supported for mail-enabled Security Groups or Distribution Groups
* Group owners can be allowed to manage membership for groups they own globally across the tenant or for a subset of users via allowing group(s) and can be further scoped to Office 365 Groups or Security Groups
* Users can be allowed to request to join a group in the Access Panel
* Users can be granted the right to create Security Groups or Office 365 Groups

## Group Expiration
* Supported for Office 365 Groups only
* Owners are notified of expired groups 30 days, 15 days, and one day prior to expiration and are prompted to renew
* Groups that are not renewed are deleted but can be restored for up to 30 days
* A catch-all email address can be configured to receive notifications for groups without owners
* Can be configured for all Office 365 Groups or a subset
* Groups can be configured to expire 1-365 days

# Manage Microsoft Azure AD Directory Users

## General
* User are sourced directly from Azure AD, on-premises AD, or another Azure AD Tenant/Microsoft account/Social account (i.e. Google)
* default tenant domains are named <domain>.onmicrosoft.com
* deleted users can be restored for up to 30 days
* Name and Username are required when creating a new user
* Usage Location attribute must be set prior to assigning licenses to the user

## Tenant User Settings
* Control whether users can register application with Azure AD (Users can register apps - def Yes)
* Control whether non-admins can access the AAD Admin Portal (Restrict access to Azure AD Admin portal for non-admins - def No)
* Control whether all users, specific users, or no users can associate Work or School accounts with LinkedIn (Allow users to connect work/school to LinkedIn - def Yes)
* Control whether guest users permission are limited to viewing their own profile information and group member for groups they're members of (Guest users permissions are limited - def Yes)
* Control whether Admins and Users and Guest Inviter Role can invite other guests (Admins and Users in Guest Inviter Role can invite - def Yes)
* Control whether members can invite guests to the tenant (members can invite - def Yes)
* Control whetehr guest users without Azure AD/Microsoft/social (i.e. Google) account can instead authenticate with OTP (Enable Email One-Time Passcode for Guests - def No)
* Control whether invites can be sent to all domains (Def), all but specific domains, or only a specific set of domains
* Control whether all users or a selected set of users can register and configure MFA settings and SSPR in the Access Panel (def None)

## Individual User Settings
* Set the user's first name and or last name
* set the user's job title, department, and manager
* Block the user's sign in
* Set the user's Usage Location
* Setup contact info (address and such)
* Configure minors and consent info (GDPR)
* View user's permissions over Azure resources and Assigned Apps
* Manager user's membership in Azure AD Groups and Azure AD / Office 365 Roles
* Manage user's devices
* Assign licenses directly to the user

## User Authentication Methods
* Require the user to re-register for MFA
* Revoke the user's MFA sessions
* Reset the user's password
* Setup the phone and alternate phone numbers for MFA
* Setup the email and alternate email for MFA

# Configure Authentication Methods
