# Active Directory Auditing Best Practices

***_Active Directory and AD Group Policy are foundational elements of any Microsoft Windows environment because of the critical role they play in account management, authentication, authorization, access management and operations. Accordingly, proper Active Directory auditing is essential for both cybersecurity and regulatory compliance. For example, organizations need to know who created new accounts and keep a close eye on access rights by reviewing changes to the membership of user and administrative groups._***

_To audit Active Directory, you can use either the basic (local) security audit policy settings or the advanced security audit policy settings, which enable more granularity. Microsoft does not recommend using both, since that can lead to “unexpected results in audit reporting.” In most cases, when you turn the advanced auditing on, basic auditing will be ignored, even if you later turn the advanced auditing off.  It is recommended to use Advanced auditing if you are not currently performing any auditing._
_Basic policies can be set by going to
```
Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Audit Policy.
```
```
Advanced policy settings can be found under Computer Configuration > Policies > Windows Settings > Advanced Audit Policy Configuration > Audit Policies.
```
## Audit Policy Scope
_You can define auditing policies for both the entire domain and individual organizational units (OUs). Note that a setting configured at the OU level has higher priority than a domain-level setting and will override it in case of conflicts. You can check the resulting policies using the auditpol command-line utility._

## Configuring the Security Log
You’ll also need to specify the maximum size and other properties of the Security log using the Event Logging policy settings. To change settings via GPME, navigate to Computer Configuration > Policies > Windows Settings > Security Settings > Event Log and double-click the policy name. According to Microsoft, the recommended maximum log size for modern OS versions is 4Gb, and the recommended maximum total size for all logs is 16Gb. You can view the logs with Event Viewer.

## Which AD Security Log Events to Track
_Recommended Audit Policies by Operating System
This section contains tables that list the audit setting recommendations that apply to the following operating systems:_

- Windows Server 2016
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2008
- Windows 10
- Windows 8.1
- Windows 7

_These tables contain the Windows default setting, the baseline recommendations, and the stronger recommendations for these operating systems._

## Audit Policy Tables Legend

**_Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, and Windows Server 2008 Audit Settings Recommendations:_**
## Audit account logon events

* Audit Credential Validation: Success,Failure
* Audit Kerberos Authentication Service: Success, Failure
* Audit Kerberos Service Ticket Operations: Failure
* Audit Other Account Logon Events: Success, Failure
**

## Audit logon events

* Audit Account Lockout: Success, Failure
* Audit IPsec Main Mode	Success, Failure (IF)
* Audit Group Membership: Success
* Audit Logoff: Success, Failure
* Audit Logon: Success, Failure
* Audit Special Logon: Success, Failure
* Audit Other Logon/Logoff Events: Success, Failure
* Audit Network Policy Server: Success, Failure

***

## Account management

* Audit Application Group Management: Success, Failure
* Audit Computer Account Management: Success, Failure
* Audit Distribution Group Management: Success
* Audit Other Account Management Events: Success
* Audit Security Group Management: Success, Failure
* Audit User Account Management: Success, Failure
***
## Directory service access

* Audit Directory Service Access: Success, Failure
* Audit Directory Service Changes: Success, Failure
***

## Object access

* Audit Detailed File Share: Failure
* Audit File Share: Success, Failure
* Audit Other Object Access Events: Success, Failure
* Audit Removable Storage: Success, Failure
***

## Policy change

* Audit Policy Change: Success, Failure
* Audit Authentication Policy Change: Success, Failure
* Audit MPSSVC Rule-Level Policy Change: Success, Failure
* Audit Other Policy Change Events: Failure
***

## Privilege use

* Audit Sensitive Privilege Use: Success, Failure
***

## Process tracking (sometimes called Detailed Tracking)

* Audit PNP Activity: Success
* Audit Process Creation: Success, Failure
* Audit DPAPI Activity:	Success, Failure (IF)
***

## System

* Audit Security State Change: Success, Failure
* Audit Other System Events: Success, Failure
* Audit System Integrity: Success, Failure
** Audit Security System Extension: Success, Failure
** Audit IPsec Driver: Success, Failure
***
**_Windows 10, Windows 8, and Windows 7 Audit Settings Recommendations:_**

## Audit account logon events

* Audit Credential Validation: Success, Failure
* Audit Kerberos Authentication Service: Success, Failure
* Audit Kerberos Service Ticket Operations: Failure
* Audit Other Account Logon Events: Success, Failure

***

## Audit logon events

* Audit Account Lockout: Success, Failure
* Audit Group Membership: Success, Failure
* Audit Logoff: Success, Failure
* Audit Logon: Success, Failure
* Audit Special Logon: Success, Failure
* Audit IPsec Main Mode: Success, Failure (optinal)
***

## Account management

* Audit Application Group Management: Success, Failure (optinal)
* Audit Computer Account Management: Success, Failure
* Audit Distribution Group Management: Success (optinal)
* Audit Other Account Management Events: Success, Failure 
* Audit Security Group Management: Success, Failure
* Audit User Account Management: Success, Failure
***

## Directory service access

* Audit Directory Service Access: Success, Failure (optinal)
* Audit Directory Service Changes: Success, Failure (optinal)
***

##Object access

* Audit Detailed File Share: Success, Failure (optinal)
* Audit File Share: Success, Failure (optinal)
* Audit Other Object Access Events: Success, Failure (optinal)
* Audit Removable Storage: Success, Failure
***

## Policy change

* Audit Policy Change: Success, Failure
* Audit Authentication Policy Change: Success, Failure
* Audit MPSSVC Rule-Level Policy Change: Success, Failure
* Audit Other Policy Change Events: Failure
***

## Privilege use

* Audit Sensitive Privilege Use: Success, Failure
***

## Process tracking (sometimes called Detailed tracking)

* Audit PNP Activity: Success, Failure
* Audit Process Creation: Success, Failure
* Audit DPAPI Activity: Success, Failure
***


## Documentation

> [Audit Policy Recommendations](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/audit-policy-recommendations)

> [Active Directory Auditing Best Practices](https://community.spiceworks.com/topic/2322563-active-directory-auditing-best-practices)

> [Audit Policies and Event Viewer](https://www.ultimatewindowssecurity.com/securitylog/book/page.aspx?spid=chapter2)

> [Active Directory Auditing Best Practices](https://medium.com/@juan.pablo.orphanos/domain-controllers-audit-policy-best-practices-8906abc2b682)

*** 

## FAQ

#### How can I enable auditing of AD objects?

_To enable auditing of Active Directory objects you can either:_

_Configure an audit policy on the domain controllers to log the specified events for all users._
_Configure an auditing ACL (SACL) on specific objects to monitor specific changes to them._

#### How do I configure an audit policy setting for a domain controller?

_Open the Group Policy Management Console._
_Right-click the Default Domain Controllers Policy and select Edit._
``Navigate to Computer Configuration > Policies > Windows Settings > Security Settings > Advanced Audit Policy Configuration > Audit Policies.``
_Specify the audit settings for each event category want to monitor and save your changes._
_Either wait for the policy to update automatically or run gpupdate on the DC yourself to update the policy immediately._
_Use the Windows Event Viewer to view captured events._

#### How do I configure auditing for specific AD objects?
> Open Active Directory Users and Computers.
> Navigate to the object you want to monitor and open it.
> Go to the Security tab.
> Click the Advanced button.
> Go to the Auditing tab.
> Click Add.
> Select the properties you want to monitor.
> Click OK to close each window until you are back to the main ADUC screen.
