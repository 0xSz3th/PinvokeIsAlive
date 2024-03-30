
## C# Signature:
```cs
[DllImport("advapi32.dll", CharSet=CharSet.Auto, SetLastError = true)]
static extern bool LookupAccountSid(
    string lpSystemName,
    [MarshalAs(UnmanagedType.LPArray)] byte[] Sid,
    System.Text.StringBuilder lpName,
    ref uint cchName,
    System.Text.StringBuilder ReferencedDomainName,
    ref uint cchReferencedDomainName,
    out SID_NAME_USE peUse);
```

## VB Signature:
```cs
Declare Function LookupAccountSid Lib "advapi32.dll" _
    Alias "LookupAccountSidA" ( _
    ByVal systemName As String, _
    ByVal psid As Byte(), _
    ByVal accountName As String, _
    ByRef cbAccount As Integer, _
    ByVal domainName As String, _
    ByRef cbDomainName As Integer, _
    ByRef use As Integer) As Boolean
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;
using System.Text;

namespace test
{
  class Class1
  {
    const int NO_ERROR = 0;
    const int ERROR_INSUFFICIENT_BUFFER = 122;

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
    static extern bool LookupAccountSid (
      string lpSystemName,
      [MarshalAs(UnmanagedType.LPArray)] byte[] Sid,
      StringBuilder lpName,
      ref uint cchName,
      StringBuilder ReferencedDomainName,
      ref uint cchReferencedDomainName,
      out SID_NAME_USE peUse);    

    [STAThread]
    static void Main(string[] args)
    {
      StringBuilder name = new StringBuilder();
      uint cchName = (uint)name.Capacity;
      StringBuilder referencedDomainName = new StringBuilder();
      uint cchReferencedDomainName = (uint)referencedDomainName.Capacity;
      SID_NAME_USE sidUse;
      // Sid for BUILTIN\Administrators
      byte[] Sid = new byte[] {1,2,0,0,0,0,0,5,32,0,0,0,32,2};

      int err = NO_ERROR;
      if (!LookupAccountSid(null,Sid,name,ref cchName,referencedDomainName,ref cchReferencedDomainName,out sidUse))
      {
    err = System.Runtime.InteropServices.Marshal.GetLastWin32Error();
    if (err == ERROR_INSUFFICIENT_BUFFER)
    {
      name.EnsureCapacity((int)cchName);
      referencedDomainName.EnsureCapacity((int)cchReferencedDomainName);
      err = NO_ERROR;
      if (!LookupAccountSid(null,Sid,name,ref cchName,referencedDomainName,ref cchReferencedDomainName,out sidUse))
        err = System.Runtime.InteropServices.Marshal.GetLastWin32Error();
    }
      }
      if (err == 0)
    Console.WriteLine(@"Found account {0} : {1}\{2}",sidUse,referencedDomainName.ToString(),name.ToString());
      else
    Console.WriteLine(@"Error : {0}",err);
    }
  }
}
```

## VB.NET Example:
```cs
Private Shared Function MyLookupAccountSid(ByRef i_Sid() As Byte) As String

    'Input format is the format returned from "ConvertStringSidToSid"
    'Note; This function needs some work. For example, checking l_Result for error codes!

    Dim result As String = ""
    Try
        '****************************************************************
        '* Declares
        '****************************************************************

        Dim l_Result As Long
        Dim l_use As Long
        Dim l_UserName As String
        Dim l_Domain As String
        Dim l_UserNameLength As Integer = 0
        Dim l_DomainLength As Integer = 0

        '****************************************************************
        '* First call, populate l_UserNameLength and l_DomainLength
        '****************************************************************

        l_Result = LookupAccountSid(Nothing, i_Sid, l_UserName, l_UserNameLength, l_Domain, l_DomainLength, l_use)

        '****************************************************************
        '* Allocate space
        '****************************************************************

        l_UserName = Strings.StrDup(l_UserNameLength + 1, " ")  'Need space for terminating chr(0)?
        l_Domain = Strings.StrDup(l_DomainLength + 1, " ")

        '****************************************************************
        '* Fetch username and domain
        '****************************************************************

        l_Result = LookupAccountSid(Nothing, i_Sid, l_UserName, l_UserNameLength, l_Domain, l_DomainLength, l_use)

        '****************************************************************
        '* Build result
        '****************************************************************

        result = l_Domain.Substring(0, l_DomainLength) & "\" & l_UserName.Substring(0, l_UserNameLength)

    Catch ex As Exception
        result = ""
    End Try

    Return result

    End Function
```

## Alternative Managed API:
```cs
using System.Security.Principal;

    // convert the user sid to a domain\name
    string account = new SecurityIdentifier(stringSid).Translate(typeof(NTAccount)).ToString();
```
