
## C# S i g n a t u r e :
```cs
[DllImport("winspool.drv",CharSet = CharSet.Auto, SetLastError = true)]
static extern bool EnumPorts (string pName, uint level, IntPtr lpbPorts, uint cbBuf,ref uint pcbNeeded,ref uint pcReturned);
```

## VB Signature:
```cs
TODO
```

## Sample Code:
```cs
using System;
    using System.Runtime.InteropServices;
```

## Sample Code:
```cs
[Flags]
    public enum PortType
    {
        Write = 0x1,
        Read = 0x2,
        Redirected = 0x4,
        NetAttached = 0x8
    }
```

## Sample Code:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
    public struct PORT_INFO_2
    {
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pPortName;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pMonitorName;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pDescription;
        public PortType fPortType;
        internal uint Reserved;
    }
```

## Sample Code:
```cs
[DllImport("winspool.drv",CharSet = CharSet.Auto, SetLastError = true)]
    static extern bool EnumPorts (string pName, uint level, IntPtr lpbPorts, uint cbBuf,ref uint pcbNeeded,ref uint pcReturned);
```

## Sample Code:
```cs
public PORT_INFO_2[] GetInstalledPorts()
    {
        uint pcbNeeded = 0;
        uint pcReturned = 0;

        if (EnumPorts(null, 2, IntPtr.Zero, 0, ref pcbNeeded, ref pcReturned))
        {
        //succeeds, but must not, because buffer is zero (too small)!
        throw new Exception("EnumPorts should fail!");
        }

        int lastWin32Error = Marshal.GetLastWin32Error();
        //ERROR_INSUFFICIENT_BUFFER = 122 expected, if not -> Exception
        if (lastWin32Error != 122)
        {
        throw new Win32Exception(lastWin32Error);
        }

        IntPtr pPorts = Marshal.AllocHGlobal((int) pcbNeeded);
        if (EnumPorts(null, 2, pPorts, pcbNeeded, ref pcbNeeded, ref pcReturned))
        {
        IntPtr currentPort = pPorts;
        PORT_INFO_2[] pinfo = new PORT_INFO_2[pcReturned];


        for (int i = 0; i < pcReturned; i++)
        {
            pinfo[i] = (PORT_INFO_2)Marshal.PtrToStructure(currentPort, typeof(PORT_INFO_2));
            currentPort = (IntPtr) (currentPort.ToInt32() + Marshal.SizeOf(typeof (PORT_INFO_2)));           
        }
        Marshal.FreeHGlobal(pPorts);

        return pinfo;
        }

        throw new Win32Exception(Marshal.GetLastWin32Error());
    }
```
