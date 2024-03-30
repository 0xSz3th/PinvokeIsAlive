
## C# Signature:
```cs
[DllImport("Netapi32.dll", CharSet=CharSet.Unicode, ExactSpelling=true)]
    private extern static int NetUserGetInfo(
        [MarshalAs(UnmanagedType.LPWStr)] string ServerName,
        [MarshalAs(UnmanagedType.LPWStr)] string UserName, 
        int level, 
        out IntPtr BufPtr);
```

## VB Signature:
```cs
Private Declare Function NetUserGetInfo Lib "Netapi32.dll" ( _
        ByVal ServerName As String, _
        ByVal UserName As String, _
        ByVal level As Integer, _
        ByRef BufPtr As IntPtr) As Integer
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    public struct USER_INFO_10
    {
        [MarshalAs(UnmanagedType.LPWStr)]
        public string usri10_name;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string usri10_comment;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string usri10_usr_comment;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string usri10_full_name;
    }
```

## Sample Code:
```cs
public bool AccountGetFullName(string MachineName, string AccountName, ref string FullName) 
        {
            if (MachineName.Length == 0 ) 
            {
                throw new ArgumentException("Machine Name is required");
            }
            if (AccountName.Length == 0 ) 
            {
                throw new ArgumentException("Account Name is required");
            }
            try 
            {
                // Create an new instance of the USER_INFO_1 struct
                USER_INFO_10 objUserInfo10 = new USER_INFO_10();
                IntPtr bufPtr; // because it's an OUT, we don't need to Alloc
                int lngReturn = NetUserGetInfo(MachineName, AccountName, 10, out bufPtr ) ;
                if (lngReturn == 0) 
                {
                    objUserInfo10 = (USER_INFO_10) Marshal.PtrToStructure(bufPtr, typeof(USER_INFO_10) );
                    FullName = objUserInfo10.usri10_full_name;
                }
                NetApiBufferFree( bufPtr );
                bufPtr = IntPtr.Zero;
                if (lngReturn == 0 ) 
                {
                    return true;
                }
                else 
                {
                    //throw new System.ApplicationException("Could not get user's Full Name.");
                    return false;
                }
            } 
            catch (Exception exp)
            {
                Debug.WriteLine("AccountGetFullName: " + exp.Message);
                return false;
            }
        }
```

## Sample Code:
```cs
Private Declare Function NetUserGetInfo Lib "Netapi32.dll" ( _
     ByVal ServerName As String, _
     ByVal UserName As String, _
     ByVal level As Integer, _
     ByRef BufPtr As IntPtr) As Integer

    Declare Unicode Function NetApiBufferFree Lib "netapi32.dll" _
    (ByRef buffer As IntPtr) As Long
```

## Sample Code:
```cs
Public Structure USER_INFO_10
    <MarshalAs(UnmanagedType.LPWStr)> _
    Public usri10_name As String
    <MarshalAs(UnmanagedType.LPWStr)> _
    Public usri10_comment As String
    <MarshalAs(UnmanagedType.LPWStr)> _
       Public usri10_usr_comment As String
    <MarshalAs(UnmanagedType.LPWStr)> _
    Public usri10_full_name As String
    End Structure
```

## Sample Code:
```cs
Public Function AccountGetFullName(ByVal MachineName As String, ByVal AccountName As String, ByRef FullName As String) As Boolean
    If MachineName.Length = 0 Then
        Throw New ArgumentException("MachineName is Required")
    End If
    If AccountName.Length = 0 Then
        Throw New ArgumentException("AccountName is Required")
    End If
    Try
        Dim objUserInfo10 As New USER_INFO_10
        Dim bufPtr As IntPtr
        Dim lngReturn As Integer = NetUserGetInfo(MachineName, AccountName, 10, bufPtr)
        If lngReturn = 0 Then
        objUserInfo10 = CType(Marshal.PtrToStructure(bufPtr, GetType(USER_INFO_10)), USER_INFO_10)
        FullName = objUserInfo10.usri10_full_name
        End If
        Call NetApiBufferFree(bufPtr)
        bufPtr = IntPtr.Zero
        If lngReturn = 0 Then
        Return True
        Else
        Return False
        End If
    Catch exp As Exception
        MsgBox("AccountGetFullName: " + exp.Message)
        Return False
    End Try
    End Function
```
