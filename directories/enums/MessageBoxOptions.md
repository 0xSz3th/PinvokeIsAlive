
## C# Definition:
```cs
///<summary>
/// Flags that define appearance and behaviour of a standard message box displayed by a call to the MessageBox function.
/// </summary>    
[Flags] 
public enum MessageBoxOptions : uint
{
     OkOnly         = 0x000000,
     OkCancel       = 0x000001,
     AbortRetryIgnore   = 0x000002,
     YesNoCancel    = 0x000003,
     YesNo          = 0x000004,
     RetryCancel    = 0x000005,
     CancelTryContinue  = 0x000006,
     IconHand       = 0x000010,
     IconQuestion       = 0x000020,
     IconExclamation    = 0x000030,
     IconAsterisk       = 0x000040,
     UserIcon       = 0x000080,
     IconWarning    = IconExclamation,
     IconError      = IconHand,
     IconInformation    = IconAsterisk,
     IconStop       = IconHand,
     DefButton1     = 0x000000,
     DefButton2     = 0x000100,
     DefButton3     = 0x000200,
     DefButton4     = 0x000300,
     ApplicationModal   = 0x000000,
     SystemModal    = 0x001000,
     TaskModal      = 0x002000,
     Help           = 0x004000,
     NoFocus        = 0x008000,
     SetForeground      = 0x010000,
     DefaultDesktopOnly = 0x020000,
     Topmost        = 0x040000,
     Right          = 0x080000,
     RTLReading     = 0x100000
}
```

## VB.NET Definition:
```cs
'''<summary>
''' Flags that define appearance and behaviour of a standard message box displayed by a call to the MessageBox function.
''' </summary>    
<Flags> _
Public Enum MessageBoxOptions As UInteger
     OkOnly         = &H000000
     OkCancel       = &H000001
     AbortRetryIgnore   = &H000002
     YesNoCancel    = &H000003
     YesNo          = &H000004
     RetryCancel    = &H000005
     CancelTryContinue  = &H000006
     IconHand       = &H000010
     IconQuestion       = &H000020
     IconExclamation    = &H000030
     IconAsterisk       = &H000040
     UserIcon       = &H000080
     IconWarning    = IconExclamation
     IconError      = IconHand
     IconInformation    = IconAsterisk
     IconStop       = IconHand
     DefButton1     = &H000000
     DefButton2     = &H000100
     DefButton3     = &H000200
     DefButton4     = &H000300
     ApplicationModal   = &H000000
     SystemModal    = &H001000
     TaskModal      = &H002000
     Help           = &H004000
     NoFocus        = &H008000
     SetForeground      = &H010000
     DefaultDesktopOnly = &H020000
     Topmost        = &H040000
     Right          = &H080000
     RTLReading     = &H100000
End Enum
```

## VB Definition:
```cs
Public Enum MessageBoxOptions 
     OkOnly         As Long = &H000000
     OkCancel       As Long = &H000001
     AbortRetryIgnore   As Long = &H000002
     YesNoCancel    As Long = &H000003
     YesNo          As Long = &H000004
     RetryCancel    As Long = &H000005
     CancelTryContinue  As Long = &H000006
     IconHand       As Long = &H000010
     IconQuestion       As Long = &H000020
     IconExclamation    As Long = &H000030
     IconAsterisk       As Long = &H000040
     UserIcon       As Long = &H000080
     IconWarning    As Long = IconExclamation
     IconError      As Long = IconHand
     IconInformation    As Long = IconAsterisk
     IconStop       As Long = IconHand
     DefButton1     As Long = &H000000
     DefButton2     As Long = &H000100
     DefButton3     As Long = &H000200
     DefButton4     As Long = &H000300
     ApplicationModal   As Long = &H000000
     SystemModal    As Long = &H001000
     TaskModal      As Long = &H002000
     Help           As Long = &H004000
     NoFocus        As Long = &H008000
     SetForeground      As Long = &H010000
     DefaultDesktopOnly As Long = &H020000
     Topmost        As Long = &H040000
     Right          As Long = &H080000
     RTLReading     As Long = &H100000
End Enum
```
