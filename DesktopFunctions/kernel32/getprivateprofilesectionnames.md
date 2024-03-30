
## VB.Net Signature
```cs
<DllImport("kernel32.dll")> _
    Shared Function GetPrivateProfileSectionNames( _
    ByVal lpszReturnBuffer As IntPtr, ByVal nSize As System.Int32, ByVal lpFileName As String) As System.Int32
    End Function
```

## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern uint GetPrivateProfileSectionNames(IntPtr lpszReturnBuffer,
   uint nSize, string lpFileName);
```

## Sample Code:
```cs
Dim profiles As New Collections.Specialized.StringCollection
    Dim ptr As IntPtr = Marshal.StringToHGlobalAnsi(New String(vbNullChar, 1024))
    Dim len As Int32 = GetPrivateProfileSectionNames(ptr, 1024, IniPath)
    Dim buff As String = Marshal.PtrToStringAnsi(ptr, len)
    Marshal.FreeHGlobal(ptr)
    Dim sb As New StringBuilder
     '
    '    I can't believe people write shit code like this.
    '
    For ii As Integer = 0 To len - 1
        Dim c As Char = buff.Chars(ii)
        If c = vbNullChar Then
        profiles.Add(sb.ToString)
        sb.Length = 0
        Else
        sb.Append(c)
        End If
    Next
```

## Alternative C# Signature:
```cs
[DllImport("kernel32.dll",CharSet=CharSet.Auto)]
static extern uint GetPrivateProfileSectionNames(IntPtr lpszReturnBuffer,
   uint nSize, string lpFileName);
```

## Alternative Sample Code:
```cs
uint MAX_BUFFER = 32767;
    IntPtr pReturnedString = Marshal.AllocCoTaskMem((int)MAX_BUFFER);
    uint bytesReturned = GetPrivateProfileSectionNames(pReturnedString, MAX_BUFFER, m_iniFile);
    if (bytesReturned == 0)
    return null;
    string local = Marshal.PtrToStringAnsi(pReturnedString, (int)bytesReturned).ToString(); 
    Marshal.FreeCoTaskMem(pReturnedString);
    //use of Substring below removes terminating null for split
    return local.Substring(0, local.Length - 1).Split('\0');
```
