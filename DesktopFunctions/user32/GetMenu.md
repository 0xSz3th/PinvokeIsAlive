
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr GetMenu(IntPtr hWnd);
```

## Sample Code:
```cs
public const UInt32 MF_BYPOSITION = 0x00000400;

//Delete Menu Item
IntPtr hWnd = FindWindow("WindowClass", "WindowName");
if (hWnd.ToInt32() != 0) {
     IntPtr hMenu = GetMenu(hWnd);
     if (hMenu.ToInt32() != 0) {
     for (uint i = GetMenuItemCount(hMenu)-1; i >= 0; --i) {
         StringBuilder menuName = new StringBuilder(0x20);
         GetMenuString(hMenu, i, menuName, 0x20, MF_BYPOSITION);
         DeleteMenu(hMenu, i, MF_BYPOSITION);
     }
     }
}
```
