
## C# Signature:
```cs
[DllImport("Netapi32.dll")]
static extern NetApiStatus NetApiBufferFree(IntPtr Buffer);

[DllImport("Netapi32.dll", CharSet=CharSet.Unicode)]
static extern NetApiStatus NetGetDCName(string serverName, string domainName, out IntPtr buffer);
```

## VB Signature:
```cs
<DllImport("Netapi32.dll")> _
  Private Shared Function NetApiBufferFree(ByVal buffer As IntPtr) As NetApiStatus
  End Function

  <DllImport("Netapi32.dll", CharSet:=CharSet.Unicode)> _
  Private Shared Function NetGetDCName(ByVal serverName As String, ByVal domainName As String, ByRef buffer As IntPtr) As NetApiStatus
  End Function
```

## C# User-Defined Types:
```cs
public enum NetApiStatus
{
    Success = 0,
    DCNotFound = 2453
}
```

## VB User-Defined Types:
```cs
Private Enum NetApiStatus
    Success = 0
    DCNotFound = 2453
  End Enum
```

## C# Sample Code:
```cs
public static string GetDCName()
{
    IntPtr domainInfo = IntPtr.Zero;
    string dcName = String.Empty;

    try
    {
        NetApiStatus result = NetGetDCName(null, null, out domainInfo);
        if (result == NetApiStatus.Success)
        {
            dcName = Marshal.PtrToStringAuto(domainInfo);
        }
    }
    finally 
    {
        NetApiBufferFree(domainInfo);
    }

    return dcName;

}
```

## VB Sample Code:
```cs
Public Shared Function GetDCName() As String
    Dim domainInfo As IntPtr = IntPtr.Zero
    Dim dcName As String = String.Empty

    Try
      Dim result As NetApiStatus = NetGetDCName(Nothing, Nothing, domainInfo)
      If result = NetApiStatus.Success Then dcName = Marshal.PtrToStringAuto(domainInfo)
    Finally
      NetApiBufferFree(domainInfo)
    End Try

    Return dcName
  End Function
```
