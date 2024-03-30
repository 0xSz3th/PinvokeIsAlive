
## C# Signature:
```cs
public static IntPtr SetClassLong(HandleRef hWnd, int nIndex, IntPtr dwNewLong)
{
    if (IntPtr.Size > 4)
        return SetClassLongPtr64(hWnd, nIndex, dwNewLong);
    else
        return new IntPtr(SetClassLongPtr32(hWnd, nIndex, unchecked((uint)dwNewLong.ToInt32())));
}

[DllImport("user32.dll", EntryPoint="SetClassLong")]
public static extern uint SetClassLongPtr32(HandleRef hWnd, int nIndex, uint dwNewLong);

[DllImport("user32.dll", EntryPoint="SetClassLongPtr")]
public static extern IntPtr SetClassLongPtr64(HandleRef hWnd, int nIndex, IntPtr dwNewLong);
```
