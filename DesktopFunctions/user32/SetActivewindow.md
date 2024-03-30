
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
public static extern IntPtr SetActiveWindow(IntPtr hWnd);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=true)> _
Private Shared Function SetActiveWindow(ByVal hWnd As IntPtr) As IntPtr
End Function
```

## VB Signature:
```cs
Public Declare Function SetActiveWindow Lib "user32" _
         (ByVal hWnd As Long) As Long
```

## Sample Code:
```cs
[DllImport("user32.dll")]
static extern IntPtr SetActiveWindow(IntPtr hWnd);

public void MakeFormActive() 
{
    SetActiveWindow(wndHandle);
}
```
