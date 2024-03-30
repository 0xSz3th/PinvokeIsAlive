
## C# Signature:
```cs
[DllImport("user32.dll", CharSet = CharSet.Auto, SetLastError = true)]
static extern int BroadcastSystemMessageEx(uint flags, ref uint lpInfo, uint Msg, [MarshalAs(UnmanagedType.SysUInt)] ulong wParam, [MarshalAs(UnmanagedType.SysInt)] long lParam, out BSMINFO pbsmInfo);
```
