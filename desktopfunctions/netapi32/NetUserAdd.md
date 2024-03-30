
## C# Signature:
```cs
[DllImport("netapi32.dll", CharSet=CharSet.Unicode, SetLastError=true)]
private static extern int NetUserAdd(
     [MarshalAs(UnmanagedType.LPWStr)] string servername,
     UInt32 level,
     IntPtr userInfo,
     out UInt32 parm_err);
```

## VB Signature:
```cs
Private Declare Function NetUserAdd Lib "Netapi32.dll" ( _
    <MarshalAs(UnmanagedType.LPWStr)> ByVal servername As String, _
    ByVal level As Integer, _
    ByRef buf As USER_INFO_1, _
    ByRef param_error As Integer) As Integer
```

## Sample Code:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Unicode)> _
       Private Structure USER_INFO_1
    Dim Username As String
    Dim Password As String
    Dim Password_age As Integer
    Dim Priv As Integer
    Dim HomeDir As String
    Dim Comments As String
    Dim Flag As Integer
    Dim Script_Path As String
    End Structure

    Private Declare Function NetUserAdd Lib "Netapi32.dll" ( _
    <MarshalAs(UnmanagedType.LPWStr)> ByVal servername As String, _
    ByVal level As Integer, _
    ByRef buf As USER_INFO_1, _
    ByRef param_error As Integer) As Integer

   Public Shared Function AddUser(ByVal UserName As String, Optional ByVal Server As String = "") As String

    Dim NewUser As New USER_INFO_1
    Dim bufPtr As IntPtr
    Dim Out As Integer

    With NewUser
        .Comments = "New user account setup by LocalUser.dll"
        .Password = "P@ssword"
        .HomeDir = ""
        .Script_Path = ""
        .Username = UserName.Trim
        .Priv = 1
    End With

    Dim RetVal As Integer = NetUserAdd(Server, 1, NewUser, Out)

    If RetVal <> 0 Then
        Return New System.ComponentModel.Win32Exception(RetVal).Message
    Else
        Return "Success"
    End If

    End Function
```
