
## C# Signature:
```cs
[DllImport("credui.dll", CharSet = CharSet.Unicode, SetLastError = true)]
    private static extern Boolean CredPackAuthenticationBuffer(
      int dwFlags,
      string pszUserName,
      string pszPassword,
      IntPtr pPackedCredentials,
      ref int pcbPackedCredentials);
```

## VB Signature:
```cs
''' <summary>
    ''' Windows Platform function (called via pInvoke) which populates an authentication buffer with authentication details.
    ''' See http://msdn.microsoft.com/en-us/library/aa374802(v=vs.85).aspx
    ''' </summary>
    ''' <param name="dwFlags">RESERVED - must be zero.</param>
    ''' <param name="pszUserName">User Name.</param>
    ''' <param name="pszPassword">Password.</param>
    ''' <param name="pPackedCredentials">The buffer to be packed with credentials.</param>
    ''' <param name="pcbPackedCredentials">The the size of the buffer.</param>
    ''' <returns><c>True</c> on success; otherwise <c>False</c>. For extended error information, call the GetLastError() function.</returns>
    <DllImport("credui.dll", CharSet:=CharSet.Unicode, SetLastError:=True)> <CLSCompliant(False)> _
    Public Shared Function CredPackAuthenticationBuffer(ByVal dwFlags As UInt32, ByVal pszUserName As String, ByVal pszPassword As String, ByVal pPackedCredentials As IntPtr, ByRef pcbPackedCredentials As UInt32) As <MarshalAs(UnmanagedType.Bool)> Boolean
    End Function
```

## Sample Code:
```cs
string username = "User";
    string password = "";
    int inCredSize = 1024;
    IntPtr inCredBuffer = Marshal.AllocCoTaskMem(inCredSize);

    CredPackAuthenticationBuffer(0, username, password, inCredBuffer, ref inCredSize);
```
