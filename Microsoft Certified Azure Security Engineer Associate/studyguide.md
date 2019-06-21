# Manage Identity and Access
## Configure Microsoft Azure Active Directory for workloads
### Configure multi-factor authentication settings
#### General
* Available via Azure AD Premium, MFA for Office 365, and for Azure AD Global Administrators
* Users who are enforced for MFA overrides any Conditional Access policies enforcing it
* Require MFA by enforcing it on a user, configuring conditional access, or requiring it based upon sign on risk using Identity Protection
* When user is enabled for MFA, non-browser apps are unaffected and apps using modern authentication will work as long as the existing access token is valid
* Activity Report in MFA Blade in Azure AD is for Azure MFA Server only

#### Azure MFA Services vs Azure MFA Server
* MFA Services supports SaaS apps in application gallery
* MFA Services supports web apps published through AAD Proxy
* MFA Server supports IIS Apps

#### Azure MFA Authentication Factors
* Mobile App Notification
* Mobile App Verification Code
* Phone Call
* One-way SMS
* Hardware Token (OATH)

#### Azure MFA Service Configuration (MFA Portal)
* Allow/Disallow Application Passwords
* Skip MFA for Trusted IPs
* Set authentication factors
* Allow users to remember MFA authentications on trusted devices for 0-60 days (def 14)
	
#### Azure MFA Server Configuration
* One time bypass for a user
* SMS timeout (def 60 sec)
* Cache MFA for multiple authentications based on User, IP, or application
* Check MFA Server status

#### Azure MFA Service Configuration (Azure Portal)
* Lock out a user based on the number of denied MFA requests including a reset counter and lockout duration
* Block MFA for specific users in order to lock them out for 90 days (can be manually removed from this list)
* Allow users to submit Fraud Alerts when they receive MFA requests they didn’t initiate; users can be blocked automatically; setup a code (number) users can select to report fraud via phone
* Configure OATH tokens
* For phone greetings, configure the source phone number, number of pin attempts and a custom greeting

#### Azure MFA States
* Disabled
* Enabled -> User enrolled for MFA but not yet registered
* Enforced -> User enrolled for MFA and registered

#### Azure MFA User Specific Options
* Force the user to provide contact methods again
* Delete all the user’s app passwords
* Restore MFA prompts for all of the users remembered devices

#### Enable MFA For a User
* MFA Portal (Get there via Azure Portal)
* Enable via PowerShell with script below:
* Import-Module MSOnline
$st = New-Object -TypeName Microsoft.Online.Administration.StrongAuthenticationRequirement
$st.RelyingParty = "*"
$st.State = "Enabled"
$sta = @($st)
Set-MsolUser -UserPrincipalName bsimon@contoso.com -StrongAuthenticationRequirements $sta

### Manage Microsoft Azure AD directory groups

#### General
* Direct, Dynamic, or Synced
* Security Groups or Office 365 Groups
* All Users group is a dynamic group that contains all tenant users and guest users by default
* Office 365 Groups support blocking the usage of certain words in the names which can be uploaded via CSV
* Office 365 Groups support enforcing a naming convention which can add a prefix or suffix which is either a custom string or an attribute from the user who created it
* Office 365 Groups that are deleted by a user or automatically by an expiration policy can be restored for up to 30 days

#### Dynamic Groups
* Supported for both Security Groups and Office 365 Groups
* Requires Azure AD Premium P1 be associated with the Azure AD tenant
* Created for groups that will contain either Users or Devices
* Manage membership based on the user or device attributes

#### Self-Service Group Management
* Not supported for mail-enabled Security Groups or Distribution Groups
* Group owners can be allowed to manage membership for groups they own globally across the tenant or for a subset of users via allowing group(s) and can be further scoped to Office 365 Groups or Security Groups
* Users can be allowed to request to join a group in the Access Panel
* Users can be granted the right to create Security Groups or Office 365 Groups

#### Group Expiration
* Supported for Office 365 Groups only
* Owners are notified of expired groups 30 days, 15 days, and one day prior to expiration and are prompted to renew
* Groups that are not renewed are deleted but can be restored for up to 30 days
* A catch-all email address can be configured to receive notifications for groups without owners
* Can be configured for all Office 365 Groups or a subset
* Groups can be configured to expire 1-365 days

### Manage Microsoft Azure AD Directory Users

#### General
* User are sourced directly from Azure AD, on-premises AD, or another Azure AD Tenant/Microsoft account/Social account (i.e. Google)
* default tenant domains are named <domain>.onmicrosoft.com
* deleted users can be restored for up to 30 days
* Name and Username are required when creating a new user
* Usage Location attribute must be set prior to assigning licenses to the user

#### Tenant User Settings
* Control whether users can register application with Azure AD (Users can register apps - def Yes)
* Control whether non-admins can access the AAD Admin Portal (Restrict access to Azure AD Admin portal for non-admins - def No)
* Control whether all users, specific users, or no users can associate Work or School accounts with LinkedIn (Allow users to connect work/school to LinkedIn - def Yes)
* Control whether guest users permission are limited to viewing their own profile information and group member for groups they're members of (Guest users permissions are limited - def Yes)
* Control whether Admins and Users and Guest Inviter Role can invite other guests (Admins and Users in Guest Inviter Role can invite - def Yes)
* Control whether members can invite guests to the tenant (members can invite - def Yes)
* Control whetehr guest users without Azure AD/Microsoft/social (i.e. Google) account can instead authenticate with OTP (Enable Email One-Time Passcode for Guests - def No)
* Control whether invites can be sent to all domains (Def), all but specific domains, or only a specific set of domains
* Control whether all users or a selected set of users can register and configure MFA settings and SSPR in the Access Panel (def None)

#### Individual User Settings
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

#### User Authentication Methods
* Require the user to re-register for MFA
* Revoke the user's MFA sessions
* Reset the user's password
* Setup the phone and alternate phone numbers for MFA
* Setup the email and alternate email for MFA

### Configure Authentication Methods

#### General
* Keep me signed in (KMSI) sets a session cookies good for 180 days to preserve a user's login session

#### Azure AD Password Hash Sync
* Users use same username and password as on-premises
* Required by Identity Protection and Azure AD Domain Services
* Password hashes are hashed and synced to Azure AD every two minutes (sync frequency cannot be changed)
* Keep me signed in (KMSI) sets a session
* Password complexity and expiration of on-premises is honored (use case for custom password filters)
* Can be used as failover method for Passthrough Authentication and Federated Authentication but requires manual changes
* Can't limit which users in scope of a sync have passwords synced; all synced users or none
* Account that expires on-premises (accountExpires attribute) is not honored in Azure AD and the Azure AD account must be manually disabled.
* Service account used by Azure AD Connect must have Replicate Directory Changes and Replicate Directory Changes All in Windows Server Active Directory
* Express Settings of Azure AD Connect automatically configure PHS

#### Azure AD Passthrough Authentication
* Passwords do not have to be synced to Azure AD
* On-premises password policies are honored
* Lightweight agent runs on-premises on domain controllers and communicates with a proxy service running on a member server which communicates with Azure AD
* Supports on-premises UPN and Alternate Id
* Available for all SKUs of Azure AD
* Supports Azure MFA, Conditional Access Policies (limited), Self-Service Password Reset using Password Writeback
* Only Global Administrators can add PTA agents
* Use cases are when you do not want to synchronize passwords, you want to enforce on-premises security and password policies, or you want to use an Alternate ID
* Not integrated with Azure AD Connect Health so no PTA agent reporting available
* Conditional Access Policies supported include Azure MFA, Blocking Legacy authentication, and filtering brute force attacks
* Certificate Authority that signs the certificates issued to the PTA agents lives in Microsoft's cloud and is only used for this purpose

#### Azure AD Smart Lockout
* Protects against brute force attacks
* Intelligence to detect normal user behavior from an attackers
* Blocks sign-in attempts for one minute after 10 failed logins
* Capable of tracking last three password hashes used to avoid incrementing the counter when the same password is used multiple times (typical user behavior) (not available for PTA)
* Enabled by default for all Azure AD SKUs but can be customized with Basic+
* Supported for PHS and PTA
* Azure AD Admin user cannot unlock an Azure AD account locked by Smart Lockout
* When PTA is used set the AAD lockout threshold less than the on-premises AD so the account locks out in AAD and doesn't impact on-premises AD
* When PTA is used set the AAD lockout threshold counter so that on-premises does not become locked out by bad attempts in Azure AD

#### Azure AD Password Protection
* Prevents users from using commonly guessed password
* Available for both Azure AD and Windows Server AD
* Provided to all Azure AD SKUs for the global list maintained by Microsoft for Cloud Users only
* Azure AD Premium P1 or above is required to use this feature for synchronized users
* Azure AD Premium P1 or above is required to create a custom banned password list
* The custom banned password list can be enforced or audited
* Extending the service to Windows Server AD requires an agent be installed on the domain contorllers and a proxy service be installed on a member server
* Enforced during change password or reset password in Azure AD

#### Seamless Single Sign-On
* Users automatically signed in to supported applications that are integrated with Azure AD when using their corporate desktops
* Available for PTA and PHS
* User's device must be domain-joined
* Available for all Azure AD SKUs
* Provisions a service account in each Active Directory forest being sychronized to the Azure AD tenant and synchronizes the Kerberos key to Azure AD so it can decrypt Kerberos tickets sent by domain-joined devices
* Enabled via Azure AD Connect

### Install and Configure Azure AD Connect
#### Azure AD Connect Health
* monitors health of Azure AD Connect Sync, AD FS, or AD DS by providing alerts, performance monitoring, and usage analytics
* Requires Azure AD Premium P1+
* Global Admins required for activation but RBAC can be used to delegate it out after activation
* Azure AD Connect Health for Sync is installed as part of Azure AD Connect
* Register-AzureADConnectHealthSyncAgent, Set-AzureADConnectHealthProxySettings, Test-AzureADConnectHealthConnectivity

#### Azure AD Connect General
* Filter what is synchronized by domain, OU, non-nested groups, or attribute
* Prevent accidental deletions from Azure AD by capping to 500 per sync which can be modified by using Enable-ADSyncExportDeletionThreshold cmdlet

#### Azure AD Connect Express Installation
* Suitable for <100,000 objects
* Automatic upgrade
* Password Hash Synchronization
* All users, groups, contacts, and WIndows 10 Computers and domains/OUs synced
* Features and scoped synchronization can be configured after initial installation

#### Azure AD Connect Custom Installation
* Useful for multiple forests or where there are >100,000 objects
* Federated or PTA
* Group-based filters

#### Azure AD Connect User Sign-In Config Options
* PHS
* PTA
* Federation with AD FS
* Federation with PingFederate
* Do not configure (3rd party federation)
* OPTIONAL (Enable Single Sign-on AKA Seamless SSO)

#### Azure AD Connect User Uniqueness
* Determine how users are represented in forest for joins in metaverse
* Users represented once across all forests being synchronized
* Join on the mail attribute
* ObjectSID and msExchangeMasterAccountSID/msRTCSIP-OriginatorSID (Exchange resource forest use case)
* sAMAccountName + MailNickName
* Specific attribute
* Source anchor can be automatically configured (ms-DS-ConsistencyGuid method) or specified 

#### Azure AD Connect Features
* Exchange Hybrid Deployment
* Exchange Mail Public Folders
* Azure AD App and attribute filters (tailoered attribute sync based on application being used in Azure AD)
* PHS (failover from PTA/Federation)
* Password Writeback
* Group Writeback
* Device Writeback
* Directory extension attribute sync (extend Azure AD schema)

# Secure data and applications
## Configure and manage Key Vault

### General Key Vault
* Standard SKUs use keys processed by software and are considered FIPS 140-2 Level 1
* Premium SKUs use keys processed by hardware (HSM) and are considered FIPS 140-2 Level 2
* Keys processed in software are encrypted at rest using system key that is stored in HSM
* Supports Sign hash and Verify hash, Key Encryption / Wrapping, and Encrypt and Decrypt
* Keys can be backup and restored from Key Vault to another Key Vault within the same region and subscription
* Not yet valid or expired keys can be used for decrypt, unwrap, and verify to allow for testing and recovery scenarios
* Integrated with DigiCert and GlobalSign

### Manage Access To Key Vault
* Two SKUs standard and premium where premium allows for use of HSM
* Supports VNet Service Endpoints
* Vault endpoints end with vault.azure.net
* Vault items use an endpoint with the following format https://{keyvault-name}.vault.azure.net/{object-type}/{object-name}/{object-version}
* Access to management plane is controlled via Azure RBAC and allows for creation, deletion, and management of Vaults as a resource
* Access to data plane is controlled via Access Policies and allows for granularity at the data type (secret, key, certificate)
* Restrict network access using firewall functionality to allow specific IPs, VNets, and allow Microsoft Services

### Manage permissions to secrets, certificates, and keys
* Data plane access groups permissions under vault resource type (secret, certificate, key) and splits operations into Management and Privileged operations
* Permissions cannot be configured on a per secret/certificate/key like AWS KMS

### Manage Certificates
* Create certificates directly in Key Vault or import them
* Supports automatic renewal with selected issuers
* Certificate and private key can be exported if that option is chosen when certificate is created/imported
* Key Vault certificate policy must be provided when certificate is generated in Key Vault to provide information such as lifecyle triggeres (email or renewal)
* Integrated with DigiCert and GlobalSign
* Certificate contacts can be set tp be notified about lifecycle events

### Configure Key Rotation
* Key Vault can manage rotation of Storage Account Keys for both ARM and Classic Storage Accounts
* Key rotation outside of certificates and Storage Accounts can be performed manually, programatically through an API, or using an Azure Automation Script


