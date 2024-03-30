
## C# Signature:
```cs
[DllImport("user32.dll", CharSet = CharSet.Auto)]
static extern bool AppendMenu(IntPtr hMenu, MenuFlags uFlags, uint uIDNewItem, string lpNewItem);
```

## VB Signature:
```cs
<DllImport("user32.dll", CharSet = CharSet.Auto)>_
Shared Function AppendMenu(ByVal hMenu As IntPtr, ByVal uFlags As MenuFlags, ByVal uIDNewItem As Int32, ByVal lpNewItem As String) As Boolean
```

## VB Signature:
```cs
[Flags]
public enum MenuFlags : uint
{
     MF_STRING = 0,
     MF_BYPOSITION = 0x400,
     MF_SEPARATOR = 0x800,
     MF_REMOVE = 0x1000,
}
```

## VB Signature:
```cs
<Flags()> _
    Public Enum MenuFlags As Integer
    MF_BYPOSITION = 1024
    MF_REMOVE = 4096
    MF_SEPARATOR = 2048
    MF_STRING = 0
    End Enum
```

## Sample Code:
```cs
<DllImport("user32.dll", CallingConvention:=CallingConvention.Cdecl)> _
    Private Shared Function GetSystemMenu(ByVal hWnd As IntPtr, ByVal bRevert As Boolean) As IntPtr
    End Function

    <Flags()> _
    Public Enum MenuFlags As Integer
        MF_BYPOSITION = 1024
        MF_REMOVE = 4096
        MF_SEPARATOR = 2048
        MF_STRING = 0
    End Enum

<DllImport("user32.dll", CharSet:=CharSet.Auto)> _
    Shared Function AppendMenu(ByVal hMenu As IntPtr, ByVal uFlags As MenuFlags, ByVal uIDNewItem As Int32, ByVal lpNewItem As String) As Boolean
    End Function

    Private Sub insertMenu(ByVal strMenuItem As String)
        Dim hMenu = GetSystemMenu(Me.Handle, False)
        AppendMenu(hMenu, MenuFlags.MF_STRING, 2, strMenuItem)
    End Sub
```
