
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool GetClientRect(IntPtr hWnd, out RECT lpRect);
```

## VB Signature:
```cs
<DllImport("user32.dll", CharSet:=CharSet.Auto)> _
Private Shared Function GetClientRect(ByVal hWnd As System.IntPtr, _
   ByRef lpRECT As RECT) As Integer
    ' Leave function empty     
End Function
```

## Tips & Tricks:
```cs
public static RECT GetClientRect(IntPtr hWnd)
{
    RECT result;
    GetClientRect(hWnd, out result);
    return result;
}

Usage
RECT clientRect = GetClientRect(handle);
```
