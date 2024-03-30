
## C# Signature:
```cs
[DllImport("user32.dll", CharSet=CharSet.Auto)]
public static extern int GetScrollPos(IntPtr hWnd, System.Windows.Forms.Orientation nBar);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", CharSet:=CharSet.Auto)> _
Public Shared Function GetScrollPos(hWnd As IntPtr,  _
          <MarshalAs(UnmanagedType.I4)>nBar As SBOrientation) As Integer
End Function
```

## VB Signature:
```cs
Public Declare Function GetScrollPos Lib "user32" _
         (ByVal hWnd As Long, _
          ByVal nBar As SBOrientation) As Long
```

## C# Sample Code:
```cs
/// <summary>
/// Gets and Sets the Horizontal Scroll position of the control.
/// </summary>
public int HScrollPos
{
     get { return GetScrollPos((IntPtr) this.Handle, System.Windows.Forms.Orientation.Horizontal); }
     set { SetScrollPos((IntPtr) this.Handle, System.Windows.Forms.Orientation.Horizontal, value, true); }
}

/// <summary>
/// Gets and Sets the Vertical Scroll position of the control.
/// </summary>
public int VScrollPos
{
     get { return GetScrollPos((IntPtr) this.Handle, System.Windows.Forms.Orientation.Vertical); }
     set { SetScrollPos((IntPtr) this.Handle, System.Windows.Forms.Orientation.Vertical, value, true); }
}
```
