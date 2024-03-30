
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool GetProcessTimes(IntPtr hProcess, out FILETIME
   lpCreationTime, out FILETIME lpExitTime, out FILETIME lpKernelTime,
   out FILETIME lpUserTime);
```

## Sample Code:
```cs
// www.dotnetnews.com

[STAThread]
static void Main(string[] args)
{
    Console.WriteLine("Enter PID:");
    int i = Convert.ToInt32( Console.ReadLine() );
    IntPtr ip = System.Diagnostics.Process.GetProcessById(i).Handle;
    System.Runtime.InteropServices.FILETIME ftCreation, ftExit, ftKernel, ftUser;

    Console.WriteLine(GetProcessTimes(ip, out ftCreation, out ftExit, out ftKernel, out ftUser));
    Console.WriteLine("Creation {0}", FiletimeToDateTime(ftCreation));
    Console.WriteLine("Exit {0}", FiletimeToDateTime(ftExit));
    Console.WriteLine("Kernel {0}", FiletimeToTimeSpan(ftKernel));
    Console.WriteLine("User {0}", FiletimeToTimeSpan(ftUser));

    Console.ReadLine();
}

[DllImport("kernel32.dll")]
static extern bool GetProcessTimes(IntPtr hProcess, 
    out System.Runtime.InteropServices.FILETIME lpCreationTime, 
    out System.Runtime.InteropServices.FILETIME lpExitTime, 
    out System.Runtime.InteropServices.FILETIME lpKernelTime,
    out System.Runtime.InteropServices.FILETIME lpUserTime);
```

## Sample Code:
```cs
public static DateTime FiletimeToDateTime(System.Runtime.InteropServices.FILETIME fileTime) 
{
    //NB! uint conversion must be done on both fields before ulong conversion
    ulong hFT2 = unchecked((((ulong)(uint)fileTime.dwHighDateTime) << 32) | (uint)fileTime.dwLowDateTime);
    return DateTime.FromFileTimeUtc((long)hFT2);
}

public static TimeSpan FiletimeToTimeSpan(System.Runtime.InteropServices.FILETIME fileTime) 
{
    //NB! uint conversion must be done on both fields before ulong conversion
    ulong hFT2 = unchecked((((ulong)(uint)fileTime.dwHighDateTime) << 32) | (uint)fileTime.dwLowDateTime);
    return TimeSpan.FromTicks((long)hFT2);
}
```
