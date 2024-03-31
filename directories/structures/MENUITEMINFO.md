
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
class MENUITEMINFO {
   public Int32 cbSize = Marshal.SizeOf(typeof(MENUITEMINFO));
   public MIIM fMask;
   public UInt32 fType;
   public UInt32 fState;
   public UInt32 wID;
   public IntPtr hSubMenu;
   public IntPtr hbmpChecked;
   public IntPtr hbmpUnchecked;
   public IntPtr dwItemData;
   public string dwTypeData = null;
   public UInt32 cch; // length of dwTypeData
   public IntPtr hbmpItem;

   public MENUITEMINFO() { }
   public MENUITEMINFO(MIIM pfMask) {
     fMask = pfMask;
   }
}
```

## VB.Net Signature:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
Public Class MENUITEMINFO
    Public cbSize As Int32 = Marshal.SizeOf(GetType(MENUITEMINFO))
    Public fMask As MIIM
    Public fType As UInt32
    Public fState As UInt32
    Public wID As UInt32
    Public hSubMenu As IntPtr
    Public hbmpChecked As IntPtr
    Public hbmpUnchecked As IntPtr
    Public dwItemData As IntPtr
    Public dwTypeData As String = Nothing
    Public cch As UInt32
    Public hbmpItem As IntPtr
End Class
```
