
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern uint WinExec(string lpCmdLine, uint uCmdShow);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll")> _
Public Function WinExec(ByVal lpCmdLine As String, ByVal uCmdShow As System.UInt32) As System.UInt32
End Function
```

## Sample Code:
```cs
Dim SW_HIDE As System.UInt32 = Decimal.ToUInt32(0)
    Dim SW_SHOW As System.UInt32 = Decimal.ToUInt32(5)

    WinExec(strFilename, SW_SHOW)
```

## Sample Code:
```cs
Unit u=new Unit();//edit by m.r.Chabi
    WinExec("control timedate.cpl",u);  // will show the time and date settings window
```
