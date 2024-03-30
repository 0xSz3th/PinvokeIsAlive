
## C# Signature:
```cs
[DllImport("advapi32.dll", CharSet=CharSet.Auto)]
static extern uint SetNamedSecurityInfo(
    string pObjectName,
    SE_OBJECT_TYPE ObjectType,
    SECURITY_INFORMATION SecurityInfo,
    IntPtr psidOwner,
    IntPtr psidGroup,
    IntPtr pDacl,
    IntPtr pSacl);
```

## VB Signature:
```cs
Declare Function SetNamedSecurityInfo Lib "advapi32.dll" ( _
    ByVal pObjectName As String, _
    ByVal ObjectType As SE_OBJECT_TYPE, _
    ByVal SecurityInfo As SECURITY_INFORMATION, _
    ByVal psidOwner As IntPtr, _
    ByVal psidGroup As IntPtr, _
    ByVal pDacl As IntPtr, _
    ByVal pSacl As IntPtr) As Integer
```

## C# Sample Code:
```cs
[DllImport("advapi32.dll", CharSet = CharSet.Unicode)]
private static extern uint SetNamedSecurityInfoW(String pObjectName, SE_OBJECT_TYPE ObjectType, SECURITY_INFORMATION SecurityInfo, IntPtr psidOwner, IntPtr psidGroup, IntPtr pDacl, IntPtr pSacl);

[DllImport("Advapi32.dll", SetLastError = true)]
private static extern bool ConvertStringSidToSid(String StringSid, ref IntPtr Sid);

private enum SE_OBJECT_TYPE 
{
    SE_UNKNOWN_OBJECT_TYPE=0,     
    SE_FILE_OBJECT, 
    SE_SERVICE, 
    SE_PRINTER,
    SE_REGISTRY_KEY,
    SE_LMSHARE,
    SE_KERNEL_OBJECT,
    SE_WINDOW_OBJECT,
    SE_DS_OBJECT,
    SE_DS_OBJECT_ALL,
    SE_PROVIDER_DEFINED_OBJECT,
    SE_WMIGUID_OBJECT,S E_REGISTRY_WOW64_32KEY
}

[Flags] private enum SECURITY_INFORMATION : uint 
{ 
    Owner = 0x00000001,
    Group = 0x00000002,
    Dacl = 0x00000004,
    Sacl = 0x00000008,
    ProtectedDacl = 0x80000000,
    ProtectedSacl = 0x40000000,
    UnprotectedDacl = 0x20000000,
    UnprotectedSacl = 0x10000000 
}

public static void SetFileOrFolderOwner(String objectName) //Note this is very basic and is silent on fail as I havent checked GetlastError and thrown an exception etc
{
        IntPtr sidPtr = IntPtr.Zero;
        SECURITY_INFORMATION sFlags = SECURITY_INFORMATION.Owner;

        System.Security.Principal.NTAccount  user = new System.Security.Principal.NTAccount("P1R4T3\\Harris");
        System.Security.Principal.SecurityIdentifier sid = (System.Security.Principal.SecurityIdentifier) user.Translate(typeof (System.Security.Principal.SecurityIdentifier));

        ConvertStringSidToSid(sid.ToString(), ref sidPtr);        

        SetNamedSecurityInfoW(UnicodeHeader+objectName, SE_OBJECT_TYPE.SE_FILE_OBJECT, sFlags,sidPtr , IntPtr.Zero, IntPtr.Zero, IntPtr.Zero);

    //Probably should release the IntPtr here to avoid memory leakage?????
```

## VB.Net Sample Code:
```cs
Dim pSecDesc, pNewDACL, pOldDACL As IntPtr
Dim ea As EXPLICIT_ACCESS
Dim Win32Error As Win32Exception
Dim ret As Integer

' merge this Explict Access with the existing DACL
ret = SetEntriesInAcl(1, ea, pOldDACL, pNewDACL)
If ret <> 0 Then
     Win32Error = New Win32Exception(ret)
     Throw New Exception(Win32Error.Message)
End If

' write the new Security Descriptor/DACL back
ret = SetNamedSecurityInfo(strPath, _
     SE_OBJECT_TYPE.SE_FILE_OBJECT, _
     SECURITY_INFORMATION.DACL_SECURITY_INFORMATION, _
     Nothing, Nothing, pNewDACL, Nothing)
If ret <> 0 Then
     Win32Error = New Win32Exception(ret)
     Throw New Exception(Win32Error.Message)
End If
```
