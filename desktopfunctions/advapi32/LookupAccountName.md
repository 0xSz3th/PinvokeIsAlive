
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
static extern bool LookupAccountName (
    string lpSystemName,
    string lpAccountName,
    [MarshalAs(UnmanagedType.LPArray)] byte[] Sid,
    ref uint cbSid,
    StringBuilder ReferencedDomainName,
    ref uint cchReferencedDomainName,
    out SID_NAME_USE peUse);
```

## VB .NET Signature:
```cs
<DllImport("advapi32.dll", SetLastError:=True)> _
Private Shared Function LookupAccountName(lpSystemName As String, lpAccountName As String, <MarshalAs(UnmanagedType.LPArray)> Sid As Byte(), ByRef cbSid As UInteger, ReferencedDomainName As StringBuilder, ByRef cchReferencedDomainName As UInteger, peUse As SID_NAME_USE) As Boolean
End Function
```

##  C# Sample Code:
```cs
using System;
   using System.Runtime.InteropServices;
   using System.Text;

   namespace test
   {
    class clsLookupAccountName
    {
        const int NO_ERROR = 0;
        const int ERROR_INSUFFICIENT_BUFFER = 122;
        const int ERROR_INVALID_FLAGS = 1004; // On Windows Server 2003 this error is/can be returned, but processing can still continue

        enum SID_NAME_USE 
        {
            SidTypeUser = 1,
            SidTypeGroup,
            SidTypeDomain,
            SidTypeAlias,
            SidTypeWellKnownGroup,
            SidTypeDeletedAccount,
            SidTypeInvalid,
            SidTypeUnknown,
            SidTypeComputer
        }

        [DllImport("advapi32.dll", CharSet=CharSet.Auto, SetLastError = true)]
        static extern bool LookupAccountName (
            string lpSystemName,
            string lpAccountName,
            [MarshalAs(UnmanagedType.LPArray)] byte[] Sid,
            ref uint cbSid,
            StringBuilder ReferencedDomainName,
            ref uint cchReferencedDomainName,
            out SID_NAME_USE peUse);        

        [DllImport("advapi32", CharSet=CharSet.Auto, SetLastError=true)]
        static extern bool ConvertSidToStringSid(
            [MarshalAs(UnmanagedType.LPArray)] byte [] pSID, 
            out IntPtr ptrSid);

        [DllImport("kernel32.dll")]
        static extern IntPtr LocalFree(IntPtr hMem);

        [STAThread]
        static void Main(string[] args)
        {
            string accountName = "Administrator";
            byte [] Sid = null;
            uint cbSid = 0;
            StringBuilder referencedDomainName = new StringBuilder();
            uint cchReferencedDomainName = (uint)referencedDomainName.Capacity;
            SID_NAME_USE sidUse;

            int err = NO_ERROR;
            if (!LookupAccountName(null,accountName,Sid,ref cbSid,referencedDomainName,ref cchReferencedDomainName,out sidUse))
            {
                err = Marshal.GetLastWin32Error();
                if (err == ERROR_INSUFFICIENT_BUFFER || err == ERROR_INVALID_FLAGS)
                {
                    Sid = new byte[cbSid];
                    referencedDomainName.EnsureCapacity((int)cchReferencedDomainName);
                    err = NO_ERROR;
                    if (!LookupAccountName(null,accountName,Sid,ref cbSid,referencedDomainName,ref cchReferencedDomainName,out sidUse))
                        err = Marshal.GetLastWin32Error();
                }
            }
            else
            {
                // Consider throwing an exception since no result was found
            }
            if (err == 0)
            {
                IntPtr ptrSid;
                if (!ConvertSidToStringSid(Sid,out ptrSid))
                {
                    err = Marshal.GetLastWin32Error();
                    Console.WriteLine(@"Could not convert sid to string. Error : {0}",err);
                }
                else
                {
                    string sidString = Marshal.PtrToStringAuto(ptrSid);
                    LocalFree(ptrSid);
                    Console.WriteLine(@"Found sid {0} : {1}",sidUse,sidString);
                }
            }
            else
                Console.WriteLine(@"Error : {0}",err);
        }
    }
   }
```

## VB.Net Sample Code:
```cs
Dim ret As Boolean
    Dim ptrSid As IntPtr
    Dim cbSid As Integer
    Dim ptrSidString As IntPtr
    Dim SidString As String
    Dim refDomainName As New StringBuilder
    Dim cbRefDomainName As Integer
    Dim peUse As SID_USE
```

## VB.Net Sample Code:
```cs
'First get the buffer sizes
    ret = LookupAccountName(Nothing, UserName, Nothing, cbSid, Nothing, cbRefDomainName, peUse)

    'Adjust the buffers to the needed size
    ptrSid = Marshal.AllocHGlobal(cbSid)
    refDomainName.EnsureCapacity(cbRefDomainName)

    'Get the data again, now with the changed buffers
    ret = LookupAccountName(Nothing, UserName, ptrSid, cbSid, refDomainName, cbRefDomainName, peUse)

    If ret Then
       'If return doesn't fail (ret=true) then convert the buffer data at ptrSid to the SidString)
        If ConvertSidToStringSid(ptrSid, ptrSidString) Then

           'Since ptrSidString is a memory pointer we need to make it a string
        Sid = Marshal.PtrToStringAuto(ptrSidString)
           msgBox(Sid)
           'Finally free up the memory
        LocalFree(ptrSidString)
```

## VB.Net Sample Code:
```cs
End If
    End If

    Marshal.FreeHGlobal(ptrSid)
```
