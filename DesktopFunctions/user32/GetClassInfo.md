
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
static extern Boolean GetClassInfoEx(IntPtr hInstance, String lpClassName, ref WNDCLASSEX lpWndClass);
```

## VB.NET Signature:
```cs
<DllImport("user32", SetLastError:=True)> _
Private Shared Function GetClassInfoEx(hInstance As IntPtr, lpClassName As String, ByRef lpWndClass As WNDCLASSEX) As Boolean
End Function
```

## Sample Code:
```cs
IntPtr hinstance = Marshal.GetHINSTANCE(GetType().Module);
String className = "Required Class Name";
WNDCLASSEX wndClass = new WNDCLASSEX { cbSize = (uint)Marshal.SizeOf(typeof(WNDCLASSEX)) };

if (GetClassInfoEx(hinstance, className, ref wndClass))
{
   // Class exists
}
```
