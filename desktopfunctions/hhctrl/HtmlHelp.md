
## C# Signature:
```cs
[DllImport("hhctrl.ocx", SetLastError=true)]
static extern IntPtr HtmlHelp( IntPtr hWndCaller, string helpFile, UInt32 command, Int32 data );
```

## VB Signature:
```cs
<DllImport("hhctrl.ocx", EntryPoint:="HtmlHelp", CharSet:=CharSet.Auto)> _ 
Function HTMLHelp( _ 
     ByVal hWndCaller As IntPtr, ByVal pszFile As String, _ 
     ByVal uCommand As Integer, ByVal dwData As Integer) As Integer 
End Function
```

## User-Defined Types:
```cs
Public Enum HTMLHelpCommand 
     HH_DISPLAY_TOPIC = 0 
     HH_DISPLAY_TOC = 1 
     HH_DISPLAY_INDEX = 2 
     HH_DISPLAY_SEARCH = 3 
     HH_HELP_CONTEXT = &HF 
     HH_CLOSE_ALL = &H12 
End Enum
```

## Sample Code:
```cs
HTMLHelp(Nothing, filePath, HTMLHelpCommand.HH_HELP_CONTEXT, contextID)
```

## Sample Code:
```cs
HTMLHelp(Nothing, filePath, HTMLHelpCommand.HH_DISPLAY_TOC, 0)
```
