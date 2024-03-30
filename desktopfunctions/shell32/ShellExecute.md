
## C# Signature:
```cs
[DllImport("Shell32.dll", CharSet = CharSet.Auto, SetLastError = true)]
static extern IntPtr ShellExecute(IntPtr hwnd, string lpOperation, string lpFile, string lpParameters, string lpDirectory, int nShowCmd);
```

## VB Signature:
```cs
<DllImport("Shell32", CharSet:=CharSet.Auto, SetLastError:=True)> _
Public Shared Function ShellExecute(hwnd as IntPtr, lpOperation as String, lpFile as String, pParameters as String, lpDirectory as String, nShowCmd as Integer) As IntPtr
End Function
```

## Sample Code:
```cs
//Opens a URL in the default browser
IntPtr result = ShellExecute(IntPtr.Zero, "open", "http://www.google.com", null, null, 1);
```
