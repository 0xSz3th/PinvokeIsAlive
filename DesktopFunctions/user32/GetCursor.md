
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool GetCursorPos(out POINT lpPoint);
// DON'T use System.Drawing.Point, the order of the fields in System.Drawing.Point isn't guaranteed to stay the same.
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", ExactSpelling := True, SetLastError := True)> _
    Public Shared Function GetCursorPos(ByRef lpPoint As POINT) As <MarshalAs(UnmanagedType.Bool)> Boolean
    End Function
```

## VB Signature:
```cs
Declare Function GetCursorPos Lib "user32.dll" _
   (ByRef lpPoint As POINT) as boolean

<DllImport("user32.dll")> _
   Public Function GetCursorPos(<[In](), Out()> ByRef pt As POINT) As Boolean
   End Function
```

## VB Signature:
```cs
<System.Runtime.InteropServices.StructLayout(Runtime.InteropServices.LayoutKind.Sequential)> _
   Public Structure POINT
      Public X As Integer
      Public Y As Integer

      Public Sub New(ByVal X As Integer, ByVal Y As Integer)
     Me.X = X
     Me.Y = Y
      End Sub
   End Structure
```

## Tested on Unity Engine. Sould be works on other .Net Framework/IDE:
```cs
// *************************************************************************************
using System.Collections.Generic;
using UnityEngine;
using System.Runtime.InteropServices;

public class GetCursorPosTest : MonoBehaviour 
{
    private ulong lpPoint = 0;
    [DllImport("user32.dll")] static extern bool GetCursorPos(out ulong _lpPoint);

    void LateUpdate() 
    {    
        GetCursorPos(out lpPoint);
        int _x   =   (int)( lpPoint & 0x00000000FFFFFFFF);
        ulong _y = (ulong)( lpPoint & 0xFFFFFFFF00000000) >> 32;
        Debug.Log(_x + " / " + _y );
    }
}
// *************************************************************************************
```

## Sample Code:
```cs
POINT p;
if (GetCursorPos(out p))
{
    label1.Text = Convert.ToString(p.X) + ";" + Convert.ToString(p.Y);
}
```

## Alternative Managed API:
```cs
System.Windows.Forms.Cursor.Position
```
