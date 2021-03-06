# Event ID 4690: An attempt was made to duplicate a handle to an object.
###### Version: 0

## Description
This event generates if an attempt was made to duplicate a handle to an object.

## Data Dictionary
|Standard Name|Field Name|Type|Description|Sample Value|
|---|---|---|---|---|
|user_sid|SubjectUserSid|SID|SID of account that made an attempt to duplicate a handle to an object.|`S-1-5-18`|
|user_name|SubjectUserName|UnicodeString|the name of the account that made an attempt to duplicate a handle to an object.|`DC01$`|
|user_domain|SubjectDomainName|UnicodeString|subject's domain or computer name.|`CONTOSO`|
|user_logon_id|SubjectLogonId|HexInt64|hexadecimal value that can help you correlate this event with recent events that might contain the same Logon ID, for example, "4624: An account was successfully logged on."|`0x3e7`|
|object_handle_id|SourceHandleId|Pointer|hexadecimal value of a handle which was duplicated.|`0x438`|
|process_id|SourceProcessId|Pointer|hexadecimal Process ID of the process which opened the Source Handle ID before it was duplicated.|`0x674`|
|target_object_handle_id|TargetHandleId|Pointer|hexadecimal value of the new handle (the copy of Source Handle ID).|`0xd9c`|
|target_process_id|TargetProcessId|Pointer|hexadecimal Process ID of the process which opened the Target Handle ID.|`0x4`|

## References
* [MS SOURCE](https://github.com/MicrosoftDocs/windows-itpro-docs/blob/public/windows/security/threat-protection/auditing/event-4690.md)
* [MS Security Auditing Category - Object Access](https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/advanced-security-audit-policy-settings#object-access)
* [MS Security Auditing Sub-category - Audit Handle Manipulation](https://github.com/MicrosoftDocs/windows-itpro-docs/tree/master/windows/security/threat-protection/auditing/audit-handle-manipulation.md)

## Tags
* etw_level_Informational
* etw_task_task_0
* Object Access
* Audit Handle Manipulation