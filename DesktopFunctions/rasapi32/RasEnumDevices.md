
## C# Signature:
```cs
[DllImport("rasapi32.dll", SetLastError=true,CharSet=CharSet.Auto)]
        static extern int RasEnumDevices(
            IntPtr lpRasDevInfo, 
            ref int lpcb, 
            ref int lpcDevices);
```

## Tips & Tricks:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
    public class RASDEVINFO
    {
        public const int RAS_MAXDEVICETYPE = 16;
        public const int RAS_MAXDEVICENAME  = 128;

        public int dwSize;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = RAS_MAXDEVICETYPE + 1)]
        public string szDeviceType ;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = RAS_MAXDEVICENAME + 1)]
        public string szDeviceName ;
    }
```

## Sample Code:
```cs
private RASDEVINFO[] getDevices()
        {
            RASDEVINFO[] rdiRets = new RASDEVINFO[1];

            int intRet=0;
            int lpcb = 0;
            int  lpcDevices = 0;
            IntPtr devinfo = IntPtr.Zero;

            intRet = RasEnumDevices(IntPtr.Zero,ref lpcb,ref lpcDevices);

            devinfo = Marshal.AllocHGlobal(lpcb);

            rdiRets[0] = new RASDEVINFO();
            rdiRets[0].dwSize = Marshal.SizeOf(typeof(RASDEVINFO));
            Marshal.WriteInt32(devinfo, Marshal.SizeOf(rdiRets[0]));

            intRet = RasEnumDevices(devinfo,ref  lpcb,ref lpcDevices);
            if( intRet == 0)
            {
                rdiRets = new RASDEVINFO[lpcDevices];
                for(int i=0;i<lpcDevices;i++)            
                {
                    rdiRets[i] = new RASDEVINFO();

                    Marshal.PtrToStructure(devinfo, rdiRets[i]);
                    devinfo = ( IntPtr )(devinfo.ToInt32()+ Marshal.SizeOf(rdiRets[i]));
                }                
            }
            return rdiRets;
        }
```

## Tips & Tricks:
```cs
Public Class CRasDevInfo
        Public Const RAS_MAXDEVICETYPE As Integer = 16
        Public Const RAS_MAXDEVICENAME As Integer = 128
        Public dwSize As Integer
        <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MAXDEVICETYPE + 1)> _
        Public szDeviceType As String
        <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=RAS_MAXDEVICENAME + 1)> _
        Public szDeviceName As String
    End Class
```

## Sample Code:
```cs
Dim intRet As Integer
        Dim lpcb As Integer
        Dim lpcDevices As Integer
        Dim devinfo As IntPtr
        Dim rdiRet As CRasDevInfo()
        Dim i As Integer
        RasEnumDevices(IntPtr.Zero, lpcb, lpcDevices)
        devinfo = Marshal.AllocHGlobal(lpcb)
        ReDim rdiRet(0)
        rdiRet(0) = New CRasDevInfo()
        Marshal.WriteInt32(devinfo, Marshal.SizeOf(rdiRet(0)))
        intRet = RasEnumDevices(devinfo, lpcb, lpcDevices)
        If intRet = 0 Then
        ReDim rdiRet(lpcDevices - 1)
        For i = 0 To lpcDevices - 1
            rdiRet(i) = New CRasDevInfo()
            Marshal.PtrToStructure(devinfo, rdiRet(i))
            devinfo = IntPtr.op_Explicit(devinfo.ToInt32() + Marshal.SizeOf(rdiRet(i)))
        Next
        Marshal.FreeHGlobal(devinfo)
        Return rdiRet
        Else
        Return Nothing
        End If
    End Function
```
