
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern int MessageBoxTimeout(IntPtr hwnd, String text, String title, uint type, Int16 wLanguageId, Int32 milliseconds);
```

## C# Signature2:
```cs
[DllImport("user32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.U4)]
private static extern uint MessageBoxTimeout(IntPtr hwnd,
    [MarshalAs(UnmanagedType.LPTStr)]  String text,
    [MarshalAs(UnmanagedType.LPTStr)] String title,
    [MarshalAs(UnmanagedType.U4)] uint type, 
    Int16 wLanguageId, 
    Int32 milliseconds);
```

## VB.Net Signature:
```cs
Byval hWnd as IntPtr, _ 
    <MarshalAs(UnmanagedType.LPStr)> ByVal lpText as StringBuilder, _ 
    <MarshalAs(UnmanagedType.LPStr)> ByVal lpCaption as StringBuilder, _ 
    <MarshalAs(UnmanagedType.U4)> ByVal uType as UInteger, _ 
    <MarshalAs(UnmanagedType.U2)> ByVal wLanguage as Int16, _
    <MarshalAs(UnmanagedType.U4)> ByVal dwMilliseconds as Int32, _ 
    ) as <MarshalAs(UnmanagedType.U4)> UInteger
```

##  VBA Signature: 
```cs
Private Declare Function MessageBoxTimeOut _
     Lib "user32.dll" Alias "MessageBoxTimeoutA" _ 
     ( _
     Byval prmlngWindowHandle as Long, _ 
     Byval prmstrMessage as String, _
     Byval prmstrCaption as string, _
     Byval prmlngType as long, _
     Byval prmwLanguage as Integer, _
     Byval prmdwMiliseconds as Long _
     ) as Integer
```

## Sample Code:
```cs
private static uint SetupnCallMessageBoxTimeOut(IntPtr hWnd, string itsMessage, string itsCaption, uint itsMessageBoxOptions,Int32 itsTimeOutMilliSeconds)
{
     return MessageBoxTimeout(hWnd , itsMessage, itsCaption,itsMessageBoxOptions,0,itsTimeOutMilliSeconds);
}
```

## Sample Code:
```cs
private Shared Function DisplayMessageBox( _ 
       ByVal hWnd as IntPtr, _
       ByVal Message as string, _
       ByVal Caption as string, _ 
       ByVal MessageOptions as UInteger, _ 
       Byval TimeOutMilliSeconds as Int32 _ 
   ) as Uinteger

   return MessageBoxTimeOut(hWnd, New StringBuilder(Message), New StringBuilder(Caption), MessageBoxOptions,0, TimeOutMilliSeconds)

   End Function
```

## Sample Code:
```cs
Public Function DisplayMessageBox( _
    ByVal hWnd As Long, _
    ByVal Message As String, _
    ByVal Caption As String, _
    ByVal MessageBoxOptions As Long, _
    ByVal TimeOutMilliseconds As Long _
     ) As Integer

    DisplayMessageBox = MessageBoxTimeOut(hWnd, Message, Caption, MessageBoxOptions, 0, TimeOutMilliseconds)

     End Function
```
