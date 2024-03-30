
## C# Signature:
```cs
[DllImport("credui.dll", CharSet = CharSet.Auto)]   
private static extern bool CredUnPackAuthenticationBuffer(int dwFlags, IntPtr pAuthBuffer, uint cbAuthBuffer, StringBuilder pszUserName, ref int pcchMaxUserName, StringBuilder pszDomainName, ref int pcchMaxDomainame, StringBuilder pszPassword, ref int pcchMaxPassword);
```

## VB Signature:
```cs
''' <summary>
    ''' Windows Platform function (called via pInvoke) which authentication details from a packed authentication buffer.
    ''' See http://msdn.microsoft.com/en-us/library/aa375185(v=vs.85).aspx
    ''' </summary>
    ''' <param name="dwFlags">Setting the value of this parameter to CRED_PACK_PROTECTED_CREDENTIALS (1) 
    ''' specifies that the function attempts to decrypt the password before returning it in the pszPassword buffer. 
    ''' If the password cannot be decrypted, the function returns FALSE, an a call to the GetLastError function will return the value ERROR_NOT_CAPABLE.</param>
    ''' <param name="pAuthBuffer">The packed authentication buffer containing credentials to be unpacked.</param>
    ''' <param name="cbAuthBuffer">The length of the authentication buffer.</param>
    ''' <param name="pszUserName">User Name variable which will populated from the buffer.</param>
    ''' <param name="pcchMaxUserName">The maximum length of the User Name variable.</param>
    ''' <param name="pszDomainName">Domain variable which will populated from the buffer.</param>
    ''' <param name="pcchMaxDomainName">The maximum length of the Domain variable.</param>
    ''' <param name="pszPassword">Password variable which will populated from the buffer.</param>
    ''' <param name="pcchMaxPassword">The maximum length of the Password variable.</param>
    ''' <returns><c>True</c> on success; otherwise <c>False</c>. For extended error information, call the GetLastError() function.</returns>
    <DllImport("credui.dll", CharSet:=CharSet.Unicode, SetLastError:=True)> <CLSCompliant(False)> _
    Public Shared Function CredUnPackAuthenticationBuffer(ByVal dwFlags As UInt32, _
                              ByVal pAuthBuffer As IntPtr, ByVal cbAuthBuffer As UInt32, _
                              ByVal pszUserName As StringBuilder, ByRef pcchMaxUserName As UInt32, _
                              ByVal pszDomainName As StringBuilder, ByRef pcchMaxDomainName As UInt32, _
                              ByVal pszPassword As StringBuilder, ByRef pcchMaxPassword As UInt32) As <MarshalAs(UnmanagedType.Bool)> Boolean
    End Function
```

## Sample Code:
```cs
DllImport("ole32.dll")]
public static extern void CoTaskMemFree(IntPtr ptr);

[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
private struct CREDUI_INFO
{
     public int cbSize;
     public IntPtr hwndParent;
     public string pszMessageText;
     public string pszCaptionText;
     public IntPtr hbmBanner;
}  

[DllImport("credui.dll", CharSet = CharSet.Auto)]
private static extern bool CredUnPackAuthenticationBuffer(int dwFlags, IntPtr pAuthBuffer, uint cbAuthBuffer, StringBuilder pszUserName, ref int pcchMaxUserName, StringBuilder pszDomainName, ref int pcchMaxDomainame, StringBuilder pszPassword, ref int pcchMaxPassword);

[DllImport("credui.dll", CharSet = CharSet.Auto)]
private static extern int CredUIPromptForWindowsCredentials(ref CREDUI_INFO notUsedHere, int authError, ref uint authPackage, IntPtr InAuthBuffer, uint InAuthBufferSize, out IntPtr refOutAuthBuffer, out uint refOutAuthBufferSize, ref bool fSave, int flags);

public static void GetCredentialsVistaAndUp(string serverName, out NetworkCredential networkCredential)
{
     CREDUI_INFO credui = new CREDUI_INFO();
     credui.pszCaptionText = "Please enter the credentails for " + serverName;
     credui.pszMessageText = "DisplayedMessage";
     credui.cbSize = Marshal.SizeOf(credui);
     uint authPackage = 0;
     IntPtr outCredBuffer = new IntPtr();
     uint outCredSize;
     bool save = false;
     int result = CredUIPromptForWindowsCredentials(ref credui, 0,ref authPackage,IntPtr.Zero, 0, out outCredBuffer, out outCredSize, ref save, 1 /* Generic */);

     var usernameBuf = new StringBuilder(100);
     var passwordBuf  = new StringBuilder(100);
     var domainBuf = new StringBuilder(100);

     int maxUserName = 100;
     int maxDomain = 100;
     int maxPassword = 100;
     if (result == 0)
     {
     if (CredUnPackAuthenticationBuffer(0, outCredBuffer, outCredSize, usernameBuf, ref maxUserName, domainBuf, ref maxDomain, passwordBuf, ref maxPassword))
     {
         //clear the memory allocated by CredUIPromptForWindowsCredentials 
         CoTaskMemFree(outCredBuffer);
         networkCredential = new NetworkCredential()
                    {
                        UserName = usernameBuf.ToString(),
                        Password = passwordBuf.ToString(),
                        Domain = domainBuf.ToString()
                    };
         return;
       }
     }

     networkCredential = null;
}
```
