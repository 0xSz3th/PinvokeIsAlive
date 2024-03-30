
## C# Signature:
```cs
[DllImport("credui", CharSet = CharSet.Unicode)]
  private static extern CredUIReturnCodes CredUIPromptForCredentialsW(ref CREDUI_INFO creditUR, 
            string targetName,
            IntPtr reserved1,
            int iError,
            StringBuilder userName,
            int maxUserName,
            StringBuilder password,
            int maxPassword,
            [MarshalAs(UnmanagedType.Bool)] ref bool pfSave,
            CREDUI_FLAGS flags);
```

## VB .NET Signature:
```cs
Declare Function CredUIPromptForCredentialsW Lib "credui.dll" (byref creditUR AS CREDUI_INFO, _
                            byval targetName as string, _
                            byval reserved1 as IntPtr, _
                            byval iError as int32, _
                            byval UserName as StringBuilder, _
                            byval maxUserName AS int32, _
                            byval password AS StringBuilder, _
                            byval maxPassword as inte32, _
                            <MarshalAs(UnmanagedType.Bool)> byref pfSave AS Boolean, _
                            flags AS CREDUI_FLAGS) As CredUIReturnCodes
```

## Sample Code:
```cs
const int MAX_USER_NAME = 100;
  const int MAX_PASSWORD = 100;
  const int MAX_DOMAIN  = 100;

  public static CredUIReturnCodes PromptForCredentials(
            ref CREDUI_INFO creditUI,
            string targetName, 
            int netError, 
            ref string userName, 
            ref string password, 
            ref bool save, 
            CREDUI_FLAGS flags)
  {

  StringBuilder user = new StringBuilder(MAX_USER_NAME);
  StringBuilder pwd = new StringBuilder(MAX_PASSWORD);
  creditUI.cbSize = Marshal.SizeOf(creditUI);

  CredUIReturnCodes result = CredUIPromptForCredentialsW(
                ref creditUI, 
                targetName, 
                IntPtr.Zero, 
                netError, 
                user, 
                MAX_USER_NAME, 
                pwd, 
                MAX_PASSWORD, 
                ref save, 
                flags);

  userName = user.ToString();
  password = pwd.ToString();

  return result;
  }


  string host = "Database Client";
  CREDUI_INFO info = new CREDUI_INFO();
  info.pszCaptionText = host;  
  info.pszMessageText = "Please Enter Your Enterprise ID";

  CREDUI_FLAGS flags = CREDUI_FLAGS.GENERIC_CREDENTIALS |
        CREDUI_FLAGS.SHOW_SAVE_CHECK_BOX |
        CREDUI_FLAGS.ALWAYS_SHOW_UI |
        CREDUI_FLAGS.EXPECT_CONFIRMATION;

  bool savePwd = false;
  CredUIReturnCodes result = PromptForCredentials(ref info, host, 0, ref username, 
                ref password, ref savePwd, flags);
```
