
## C# Signature:
```cs
[DllImport("netapi32.dll", SetLastError=true)]
public static extern int NetWkstaGetInfo(string servername, int level, out IntPtr bufptr);
```

## VB Signature:
```cs
Declare Function NetWkstaGetInfo Lib "netapi32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    public struct WKSTA_INFO_100
    {
    public int platform_id;
    public string computer_name;
    public string lan_group;
    public int ver_major;
    public int ver_minor;
    }
```

## Sample Code:
```cs
IntPtr buffer;

var ret = PInvoke.NetWkstaGetInfo(host, 100, out buffer);
var strut_size = Marshal.SizeOf(typeof (WKSTA_INFO_100));
WKSTA_INFO_100 wksta_info;

if (ret == PInvoke.ERROR_SUCCESS)
{
     wksta_info = (WKSTA_INFO_100) Marshal.PtrToStructure(buffer, typeof (WKSTA_INFO_100));

     if (!string.IsNullOrEmpty(wksta_info.computer_name))
     return wksta_info.computer_name;
}
```
