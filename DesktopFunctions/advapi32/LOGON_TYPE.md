
## C# Signature:
```cs
enum LOGON_TYPE
{
     LOGON32_LOGON_INTERACTIVE = 2,
     LOGON32_LOGON_NETWORK = 3,
     LOGON32_LOGON_BATCH = 4,
     LOGON32_LOGON_SERVICE = 5,
     LOGON32_LOGON_UNLOCK = 7,
     LOGON32_LOGON_NETWORK_CLEARTEXT = 8,
     LOGON32_LOGON_NEW_CREDENTIALS = 9
}
```

## VB Signature:
```cs
Enum LOGON_TYPE
     LOGON32_LOGON_INTERACTIVE = 2
     LOGON32_LOGON_NETWORK = 3
     LOGON32_LOGON_BATCH = 4
     LOGON32_LOGON_SERVICE = 5
     LOGON32_LOGON_UNLOCK = 7
     LOGON32_LOGON_NETWORK_CLEARTEXT = 8
     LOGON32_LOGON_NEW_CREDENTIALS = 9
End Enum
```

## Sample Code:
```cs
// Call LogonUser to get a token for the user
    IntPtr userHandle = IntPtr.Zero();
    bool loggedOn = LogonUser(
        user,
        domain,
        password,
        LogonType.Interactive,
        LogonProvider.Default,
        out userHandle);
    if(!loggedOn)
        throw new Win32Exception(Marshal.GetLastWin32Error());

    // Begin impersonating the user
    WindowsImpersonationContext impersonationContext = WindowsIdentity.Impersonate(userHandle.Token);

    DoSomeWorkWhileImpersonating();

    // Clean up
    CloseHandle(userHandle);
    impersonationContext.Undo();
```
