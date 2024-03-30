
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int GetMenuString(IntPtr hMenu, uint uIDItem,
   [Out] StringBuilder lpString, int nMaxCount, uint uFlag);
```

## User-Defined Types:
```cs
internal const UInt32 MF_BYCOMMAND    =0x00000000;
internal const UInt32 MF_BYPOSITION   =0x00000400;
```

## Sample Code:
```cs
//Delete Menu Item
IntPtr hWnd = FindWindow("WindowClass", "WindowName");
if (hWnd.ToInt32() != 0)
{
    IntPtr hMenu = GetMenu(hWnd);
    if (hMenu.ToInt32() != 0)
    {
       for (uint i = GetMenuItemCount(hMenu) - 1; i >= 0; i--)
       {
        StringBuilder menuName = new StringBuilder(0x20);
        GetMenuString(hMenu, i, menuName, menuName.Capacity, MF_BYPOSITION);
        DeleteMenu(hMenu, i, MF_BYPOSITION);
       }
    }
}
```
