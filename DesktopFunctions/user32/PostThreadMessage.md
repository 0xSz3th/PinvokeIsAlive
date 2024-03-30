
## C# Signature:
```cs
[return: MarshalAs(UnmanagedType.Bool)]
[DllImport("user32.dll", SetLastError = true)]
public static extern bool PostThreadMessage(uint threadId, uint msg, UIntPtr wParam, IntPtr lParam);
```
