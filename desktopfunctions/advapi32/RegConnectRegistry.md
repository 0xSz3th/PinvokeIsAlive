
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError = true)]
  static extern int RegConnectRegistry(string lpmachineName, int hKey, ref int phKResult);
```

## VB Signature:
```cs
Declare Auto Function RegConnectRegistry Lib "Advapi32" ( _
   ByVal lpMachineName As String, _
   ByVal hKey As IntPtr, _
   ByRef phkResult As IntPtr _
) As Integer
```

## Notes:
```cs
LONG RegConnectRegistry(
   LPCTSTR lpMachineName,
   HKEY hKey,
   PHKEY phkResult
);
```

## VB Sample Code:
```cs
' static method
Public Shared Function OpenRemoteBaseKey(ByVal Hive As RegistryHive, ByVal RemotePC As String) As RegistryKey
   Dim ret As Integer
   Dim hRemoteKey As IntPtr

   ret = RegConnectRegistry("\\" & RemotePC, New IntPtr(Hive), hRemoteKey)
   If ret <> 0 Then
     Throw New Win32Exception(ret)
   End If

   Dim ans As New RegistryKey
   ans.IsRootHive = False
   ans.hKey = hRemoteKey
   Return ans
End Function
```

## C# Sample Code:
```cs
private con;

public RemoteRegistryReader(string computerName)
{
    int iHKEY, iResult, iReturn;
    bool bOK = false;
    string sValue = string.Empty;

    iResult = ConnectToRemoteReg(@"\\" + computerName, HKEY_LOCAL_MACHINE, ref bOK);

    if (bOK)
    {
        System.Windows.Forms.MessageBox.Show("+ Result:\t" + Convert.ToString(iResult));
    }
    else
    {
        System.Windows.Forms.MessageBox.Show("- Result... ERROR!");
    }

    con = sValue; //'0' connection exists
}

private int ConnectToRemoteReg(string computerName, int HKEY, ref bool bOK)
{
    int iReturn = 0;
    int iResult = 0;

    iReturn = RegConnectRegistry(computerName, HKEY, ref iResult);

    if (iReturn == 0)
    {
        bOK = true;
        iReturn = iResult;
    }
    else
    {
        bOK = false;
    }

        return iReturn;
}
```
