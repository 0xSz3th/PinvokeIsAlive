
## C# Signature:
```cs
[DllImport("Shlwapi.dll", SetLastError=true, CharSet = CharSet.Auto)]
static extern uint AssocQueryString(AssocF flags, AssocStr str, string pszAssoc, string pszExtra, [Out] StringBuilder pszOut, ref uint pcchOut);
```

## VB Signature:
```cs
<DllImport("Shlwapi.dll", SetLastError:=True, CharSet:=CharSet.Auto)> 
Private Shared Function AssocQueryString(ByVal flags As UInteger, ByVal str As UInteger, ByVal pszAssoc As String, ByVal pszExtra As String, ByVal pszOut As Text.StringBuilder, ByRef pcchOut As UInteger) As UInteger
End Function
```

## User-Defined Types:
```cs
[Flags]
enum AssocF : uint
{
    None = 0,
    Init_NoRemapCLSID = 0x1,
    Init_ByExeName = 0x2,
    Open_ByExeName = 0x2,
    Init_DefaultToStar = 0x4,
    Init_DefaultToFolder = 0x8,
    NoUserSettings = 0x10,
    NoTruncate = 0x20,
    Verify = 0x40,
    RemapRunDll = 0x80,
    NoFixUps = 0x100,
    IgnoreBaseClass = 0x200,
    Init_IgnoreUnknown = 0x400,
    Init_FixedProgId = 0x800,
    IsProtocol = 0x1000,
    InitForFile = 0x2000,
}

enum AssocStr
{
    Command = 1,
    Executable,
    FriendlyDocName,
    FriendlyAppName,
    NoOpen,
    ShellNewValue,
    DDECommand,
    DDEIfExec,
    DDEApplication,
    DDETopic,
    InfoTip,
    QuickTip,
    TileInfo,
    ContentType,
    DefaultIcon,
    ShellExtension,
    DropTarget,
    DelegateExecute,
    SupportedUriProtocols,
    // The values below ('Max' excluded) have been introduced in W10 1511
    ProgID,
    AppID,
    AppPublisher,
    AppIconReference,
    Max
}
```

## Sample Code:
```cs
static string AssocQueryString(AssocStr association, string extension)
{
    uint length = 0;
    uint ret = AssocQueryString(AssocF.None, association, extension, null, null, ref length);
    if (ret != 1) // expected S_FALSE
    {
        throw new InvalidOperationException("Could not determine associated string, unable to get the required buffer length. Error code: " + ret);
    }

    var sb = new StringBuilder((int)length); // (length-1) will probably work too as null termination is added
    ret = AssocQueryString(AssocF.None, association, extension, null, sb, ref length);
    if (ret != 0) // expected S_OK
    {
        throw new InvalidOperationException("Could not determine associated string. Error code: " + ret);
    }

    return sb.ToString();
}
```
