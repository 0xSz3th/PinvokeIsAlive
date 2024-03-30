
## C# Signature:
```cs
/* The SHMessageBoxCheck() function is a Windows Shell API function that displays a custom messagebox with a "never ask me again" check box.  When the user checks the checkbox, the dialog never shows up again.  The shell API .dll exports this function by ordinal only.  The entrypoint  is ordinal 185 for ASCII and 191 for unicode. */

[DllImport("shlwapi.dll", EntryPoint="#185", ExactSpelling=true, PreserveSig=false)]
public static extern int SHMessageBoxCheck(
    [In] IntPtr hwnd,
    [In] String pszText,
    [In] String pszTitle,
    [In] MessageBoxCheckFlags uType,
    [In] int iDefault,
    [In] string pszRegVal
    );
```

## VB Signature:
```cs
Declare Function SHMessageBoxCheck Lib "shlwapi.dll" (TODO) As TODO
```

## Notes:
```cs
/* We use the Windows Shell function SHMessageBoxCheck, so we have to define this parallel enum of the definitions in winuser.h. */

public enum MessageBoxCheckFlags : uint
{
    MB_OK             = 0x00000000,
    MB_OKCANCEL           = 0x00000001,
    MB_YESNO          = 0x00000004,
    MB_ICONHAND           = 0x00000010,
    MB_ICONQUESTION       = 0x00000020,
    MB_ICONEXCLAMATION    = 0x00000030,
    MB_ICONINFORMATION    = 0x00000040
}
```

## Notes:
```cs
HKEY_CURRENT_USER
        Software
            Microsoft
                Windows
                    CurrentVersion
                        Explorer
                            DontShowMeThisDialogAgain
```

## Sample Code:
```cs
/* This code displays a dialog box with a "Don't show me this dialog again" checkbox and an OK button.  In normal circumstances, result will always be 0 on return. */

int result;

try 
{
    result = SHMessageBoxCheck(
        this.Handle,
        "This text fills the dialog",
        "This text is in the title bar",
        MessageBoxCheckFlags.MB_OK | MessageBoxCheckFlags.MB_ICONINFORMATION,
        0,
        "MyApplicationName.exe" // This last argument is the value of the registry key
        );
}
catch( Exception e ) 
{
// Note that the only exceptions we can get here are inter-op exceptions, I think.
    result = -1;
}

if( result == -1 ) 
{
// The dialog didn't show up, so do some alternate action here.
}
```
