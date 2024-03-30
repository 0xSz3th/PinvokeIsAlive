
## C# Signature:
```cs
[DllImport("rasapi32.dll", SetLastError=true)]
static extern uint RasGetEntryDialParams(
   string lpszPhonebook,
   [In, Out] ref RASDIALPARAMS lprasdialparams,
   out bool lpfPassword);
```

## VB Signature:
```cs
<DllImport("rasapi32.dll", CharSet:=CharSet.Auto)> _
    Public Function RasGetEntryDialParams( _
    ByVal lpszPhonebook As String, _
    <[In](), Out()> ByRef lprasdialparams As RASDIALPARAMS, _
    <Out()> ByRef lpfPassword As Boolean) As Integer
    End Function
```

## VB Signature:
```cs
Declare Function RasGetEntryDialParams Lib "rasapi32.dll" (TODO) As TODO
```

## Sample Code:
```cs
// Only this sample works on my Windows 7 + dotNET4
    [DllImport("rasapi32.dll", SetLastError = true)]
    public static extern uint RasGetEntryDialParamsW(
        string lpszPhonebook,
        IntPtr lprasdialparams,
        out bool lpfPassword);

    public RASDIALPARAMS GetDialParams() {
    var lpRasDialParams = new RASDIALPARAMS
    {
         szEntryName = "Some dial name"
    };

    // Initialize unmanged memory to hold the struct.
    IntPtr pnt = Marshal.AllocHGlobal(Marshal.SizeOf(typeof(RASDIALPARAMS)));

    // Copy the struct to unmanaged memory.
    Marshal.StructureToPtr(lpRasDialParams, pnt, true);

    bool lprPassword = false;

    var nRet = RasGetEntryDialParamsW(null, pnt, out lprPassword);
    if (nRet != 0)
    {
        // Clear unmanaged memory
        Marshal.FreeHGlobal(pnt);
        throw new Exception("Error text");
    }

    // Copy unmanaged memory to the struct.
    lpRasDialParams = (RASDIALPARAMS)Marshal.PtrToStructure(pnt, typeof(RASDIALPARAMS));

    // Clear unmanaged memory
    Marshal.FreeHGlobal(pnt);

    return lpRasDialParams;
    }
```
