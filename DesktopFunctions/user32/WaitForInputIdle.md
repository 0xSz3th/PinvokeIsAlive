
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern uint WaitForInputIdle(IntPtr hProcess, uint dwMilliseconds);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
Private Shared Function WaitForInputIdle( _
  ByVal hProcess As IntPtr, _
  ByVal dwMilliseconds As UInteger) As Integer
End Function
```
