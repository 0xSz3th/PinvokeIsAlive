
## C# Signature:
```cs
[DllImport("advapi32", CharSet=CharSet.Auto, SetLastError=true)]
static extern bool ConvertSidToStringSid(
    [MarshalAs(UnmanagedType.LPArray)] byte [] pSID, 
    out IntPtr ptrSid);

[DllImport("advapi32", CharSet = CharSet.Auto, SetLastError = true)]
static extern bool ConvertSidToStringSid(IntPtr pSid, out string strSid);
```

## C# Signature:
```cs
static extern bool ConvertSidToStringSid(
        IntPtr pSid, // binary SID
        out IntPtr strSid); // string SID
```

## VB Signature:
```cs
Declare Auto Function ConvertSidToStringSid Lib "advapi32.dll" (ByVal pSID() As Byte, _
   ByRef ptrSid As IntPtr) As Boolean
```

## Sample Code:
```cs
// C# sample
public static string GetSidString(byte[] sid)
{
   IntPtr ptrSid;
   string sidString;
   if (!ConvertSidToStringSid(sid,out ptrSid))
     throw new System.ComponentModel.Win32Exception();
   try
   {
     sidString = Marshal.PtrToStringAuto(ptrSid);
   }
   finally
   {
     LocalFree(ptrSid);
   }
   return sidString;
}
```

## Sample Code:
```cs
// Another C# Sample that converts a sid from a DirectoryEntry object

private string GetTextualSID(DirectoryEntry objGroup){
  string sSID = string.Empty;
  byte[] SID = objGroup.Properties["objectSID"].Value as byte[];
  IntPtr sidPtr = Marshal.AllocHGlobal( SID.Length);
  sSID = "";
  System.Runtime.InteropServices.Marshal.Copy(SID, 0, sidPtr, SID.Length);
  ConvertSidToStringSid((IntPtr)sidPtr, ref sSID);
  System.Runtime.InteropServices.Marshal.FreeHGlobal( sidPtr );
  return sSID;}
```

## Sample Code:
```cs
'VB Sample
Public Shared Function ByteArrayToStringSid(ByRef bArray As Byte()) As String
   Dim ptrSID As IntPtr = Nothing
   Try
     Dim sSID As String = String.Empty
     If ConvertSidToStringSid(bArray, ptrSID) = True Then
       'The PtrToStringXXX call here needs to match the CharSet used on your
       'ConvertSidToStringSid DllImport.  The default is CharSet.Ansi.
       sSID = System.Runtime.InteropServices.Marshal.PtrToStringAnsi(ptrSID)
     End If
     Return sSID
   Finally
     LocalFree(ptrSID)
   End Try
End Function
```

## Sample Code:
```cs
'Alternative VB Sample 
Public Shared Function ByteArrayToStringSid(ByRef bArray As Byte()) As String
   Dim ptrSID As IntPtr = Nothing
   Try
     Dim sSID As String = String.Empty
     If ConvertSidToStringSid(bArray, ptrSID) = True Then
       sSID = System.Runtime.InteropServices.Marshal.PtrToStringAuto(ptrSID)
     End If
     Return sSID
   Finally
     System.Runtime.InteropServices.Marshal.FreeHGlobal(ptrSID)
   End Try
End Function
```

## Alternative Managed Code:
```cs
// C# Example
private string ConvertByteToStringSid(Byte[] sidBytes)
    {
        short sSubAuthorityCount = 0;
        StringBuilder strSid = new StringBuilder();
        strSid.Append("S-");
        try
        {
        // Add SID revision.
        strSid.Append(sidBytes[0].ToString());

        sSubAuthorityCount = Convert.ToInt16(sidBytes[1]);

        // Next six bytes are SID authority value.
        if (sidBytes[2] != 0 || sidBytes[3] != 0)
        {
            string strAuth = String.Format("0x{0:2x}{1:2x}{2:2x}{3:2x}{4:2x}{5:2x}",
                           (Int16) sidBytes[2],
                           (Int16) sidBytes[3],
                           (Int16) sidBytes[4],
                           (Int16) sidBytes[5],
                           (Int16) sidBytes[6],
                           (Int16) sidBytes[7]);
            strSid.Append("-");
            strSid.Append(strAuth);
        }
        else
        {
            Int64 iVal = sidBytes[7] +
                 (sidBytes[6] << 8) +
                 (sidBytes[5] << 16) +
                 (sidBytes[4] << 24);
            strSid.Append("-");
            strSid.Append(iVal.ToString());
        }

        // Get sub authority count...
        int idxAuth = 0;
        for (int i = 0; i < sSubAuthorityCount; i++)
        {
            idxAuth = 8 + i*4;
            UInt32 iSubAuth = BitConverter.ToUInt32(sidBytes, idxAuth);
            strSid.Append("-");
            strSid.Append(iSubAuth.ToString());
        }
        }
        catch (Exception ex)
        {
        Trace.TraceWarning(ex.Message);
        throw;
        }
        return strSid.ToString();
    }
```

## Another C# Example
```cs
using System.Security.Principal;

private string ConvertSidBytesToString(byte[] sidBytes)
{
   //SecurityIdentifier is defined in the System.Security.Principal namespace.
   SecurityIdentifier si = new SecurityIdentifier(sidBytes, 0);

   return si.ToString();
}
```

## A PowerShell Example
```cs
$strSID='S-1-5-21-XXXXXXXXXX-XXXXXXXXX-XXXXXXXXXX-1026'
     $binarySid = New-Object byte[] $sid.BinaryLength
     ([System.Security.Principal.SecurityIdentifier]$strSid).GetBinaryForm($binarySid,0)
```
