
## C# Signature:
```cs
[DllImport("Shell32.dll", SetLastError = false)]
public static extern Int32 SHGetStockIconInfo(SHSTOCKICONID siid, SHGSI uFlags, ref SHSTOCKICONINFO psii);
```

## VB Signature:
```cs
Declare Function SHGetStockIconInfo Lib "Shell32.dll" (TODO) As TODO
```

## Sample Code:
```cs
SHSTOCKICONINFO sii = new SHSTOCKICONINFO();
sii.cbSize = (UInt32) Marshal.SizeOf(typeof(SHSTOCKICONINFO));

Marshal.ThrowExceptionForHR(SHGetStockIconInfo(SHSTOCKICONID.SIID_SHIELD,
     SHGSI.SHGSI_ICON | SHGSI.SHGSI_SMALLICON,
     ref sii));

// do something with sii.hIcon
```

## Sample Code:
```cs
DestroyIcon(sii.hIcon);
```

## Sample Code:
```cs
Public Shared Function GetShildIcon(iconType As SHSTOCKICONID) As IntPtr
    Dim sii As New SHSTOCKICONINFO()
    sii.cbSize = Marshal.SizeOf(GetType(SHSTOCKICONINFO))

    If SHGetStockIconInfo(iconType, SHGSI.SHGSI_ICON Or SHGSI.SHGSI_SMALLICON, sii) = 0 Then
        Return sii.hIcon
    End If
    Return IntPtr.Zero
    End Function

    Dim hIcon As IntPtr = GetShildIcon(SHSTOCKICONID.SIID_SHIELD)
    If hIcon <> IntPtr.Zero Then
        Me.Icon = Icon.FromHandle(hIcon)
        DestroyIcon(hIcon)
    End If
```
