
## C# Signature:
```cs
[DllImport("user32.dll", CharSet = CharSet.Auto)]
static extern bool GetMenuItemInfo(IntPtr hMenu, UInt32 uItem, bool fByPosition, [In,Out] MENUITEMINFO lpmii);
```

## Notes:
```cs
public const UInt32 MF_BYCOMMAND  = 0x00000000;
public const UInt32 MF_BYPOSITION = 0x00000400;
```

## Sample Code:
```cs
MENUITEMINFO mif = new MENUITEMINFO(MIIM.STRING | MIIM.ID);
bool res = GetMenuItemInfo(hMenu, 0, true, mif);
if (res) {
     ++mif.cch;
     mif.dwTypeData = new String(' ', (int)mif.cch);
     res = GetMenuItemInfo(hMenu, 0, true, mif);
}
```
