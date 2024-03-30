
## C# Signature:
```cs
[DllImport("user32.dll")]
public static extern bool GetComboBoxInfo(IntPtr hWnd, ref COMBOBOXINFO pcbi);
```

## VB.NET Signature
```cs
<DllImport("user32.dll")> _
Public Shared Function GetComboBoxInfo(ByVal hWnd As IntPtr, ByRef pcbi As COMBOBOXINFO) As Boolean
End Function
```

## User-Defined Types (C#):
```cs
[StructLayout(LayoutKind.Sequential)]
public struct COMBOBOXINFO {
    public Int32 cbSize;
    public RECT rcItem;
    public RECT rcButton;
    public ComboBoxButtonState buttonState;
    public IntPtr hwndCombo;
    public IntPtr hwndEdit;
    public IntPtr hwndList;
}

public enum ComboBoxButtonState {
    STATE_SYSTEM_NONE = 0,
    STATE_SYSTEM_INVISIBLE = 0x00008000,
    STATE_SYSTEM_PRESSED = 0x00000008
}
```

## User-Defined Types (VB.NET):
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure COMBOBOXINFO
     Public cbSize As Int32
     Public rcItem As RECT
     Public rcButton As RECT
     Public buttonState As ComboBoxButtonState
     Public hwndCombo As IntPtr
     Public hwndEdit As IntPtr
     Public hwndList As IntPtr
End Structure

Public Enum ComboBoxButtonState
     STATE_SYSTEM_NONE = 0
     STATE_SYSTEM_INVISIBLE = &H8000
     STATE_SYSTEM_PRESSED = &H8
End Enum
```

## Sample Code (C#):
```cs
COMBOBOXINFO cbi = new COMBOBOXINFO();
cbi.cbSize = System.Runtime.InteropServices.Marshal.SizeOf(cbi);
if(GetComboBoxInfo(comboBox1.Handle, ref cbi)) {
    if(cbi.hwndEdit == IntPtr.Zero) {
        throw new Exception("ComboBox must have the DropDown style!");
    }
}
```

## Sample Code (VB.NET):
```cs
Dim cbi As COMBOBOXINFO
cbi.cbSize = System.Runtime.InteropServices.Marshal.SizeOf(cbi)
If GetComboBoxInfo(comboBox1.Handle, cbi) Then
     ...
End If
```
