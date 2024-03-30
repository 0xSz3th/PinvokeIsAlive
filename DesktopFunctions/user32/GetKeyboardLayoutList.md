
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern uint GetKeyboardLayoutList(int nBuff, [Out] IntPtr [] lpList);
```

## Sample Code:
```cs
uint nElements = GetKeyboardLayoutList(0, null);
   IntPtr[] ids = new IntPtr[nElements];
   GetKeyboardLayoutList(ids.Length, ids);
```
