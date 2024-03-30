
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern int SHGetKnownFolderPath(
    [MarshalAs(UnmanagedType.LPStruct)] Guid rfid,
    uint dwFlags,
    IntPtr hToken,
    out IntPtr ppszPath); // must be freed with Marshal.FreeCoTaskMem
```

## C# Signature with marshaling:
```cs
[DllImport("shell32.dll", CharSet = CharSet.Unicode, ExactSpelling = true, PreserveSig = false)]
static extern string SHGetKnownFolderPath(
    [MarshalAs(UnmanagedType.LPStruct)] Guid rfid,
    uint dwFlags,
    IntPtr hToken = default);
```

## VB Signature:
```cs
<DllImport("shell32.dll")> _
Shared Function SHGetKnownFolderPath(
    <MarshalAs(UnmanagedType.LPStruct)> ByVal rfid As Guid,
    ByVal dwFlags As UInteger,
    ByVal hToken As IntPtr,
    ByRef ppszPath As IntPtr ' must be freed with Marshal.FreeCoTaskMem
    ) As Integer
End Function
```

## VB Signature with marshaling:
```cs
<DllImport("shell32.dll", CharSet:=CharSet.Unicode, ExactSpelling:=True, PreserveSig:=False)>
Shared Function SHGetKnownFolderPath(
    <MarshalAs(UnmanagedType.LPStruct)> ByVal rfid As Guid,
    ByVal dwFlags As UInteger,
    ByVal hToken As IntPtr
    ) As String
End Function
```

## Sample Code (C#):
```cs
// C#
using System.Runtime.InteropServices;

public static string? GetKnownFolderPath(Guid folderGuid)
{
    IntPtr ppszPath = default;
    try
    {
        int hr = SHGetKnownFolderPath(folderGuid, 0, IntPtr.Zero, out ppszPath);
        Marshal.ThrowExceptionForHR(hr); // alternatively, check success with hr >= 0
        return Marshal.PtrToStringUni(ppszPath);
    }
    finally
    {
        Marshal.FreeCoTaskMem(ppszPath);
    }
}
```

## Sample Code with marshaling (C#):
```cs
// C#
public static string GetKnownFolderPath(Guid folderGuid)
{
    return SHGetKnownFolderPath(folderGuid, 0);
}
```

## Sample Code (VB.NET):
```cs
' VB.NET
Public Shared Function GetKnownFolderPath(ByVal folderGuid As Guid) As String
    Dim ppszPath As IntPtr
    Try
        Dim hr As Integer = SHGetKnownFolderPath(folderGuid, 0, IntPtr.Zero, ppszPath)
        Marshal.ThrowExceptionForHR(hr) ' alternatively, check success with hr >= 0
        Return Marshal.PtrToStringUni(ppszPath)
    Finally
        Marshal.FreeCoTaskMem(ppszPath)
    End Try
End Function
```

## Sample Code with marshaling (VB.NET):
```cs
' VB.NET
Public Shared Function GetKnownFolderPath(ByVal folderGuid As Guid) As String
    Return SHGetKnownFolderPath(folderGuid, 0, IntPtr.Zero)
End Function
```
