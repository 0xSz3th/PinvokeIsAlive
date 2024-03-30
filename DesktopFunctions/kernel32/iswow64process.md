
## Alternative Managed API:
```cs
Environment.Is64BitOperatingSystem
```

## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true, CallingConvention = CallingConvention.Winapi)]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool IsWow64Process(
     [In] Microsoft.Win32.SafeHandles.SafeHandleZeroOrMinusOneIsInvalid hProcess,        
     [Out, MarshalAs(UnmanagedType.Bool)] out bool wow64Process
     );

[DllImport("kernel32.dll", SetLastError = true, CallingConvention = CallingConvention.Winapi)]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool IsWow64Process([In] IntPtr processHandle,
     [Out, MarshalAs(UnmanagedType.Bool)] out bool wow64Process);
```

## VB Signature:
```cs
<DllImport("Kernel32.dll", SetLastError:=True, CallingConvention:=CallingConvention.Winapi)> _
    Public Shared Function IsWow64Process( _
    ByVal hProcess As Microsoft.Win32.SafeHandles.SafeHandleZeroOrMinusOneIsInvalid, _
    ByRef wow64Process As Boolean) As <MarshalAs(UnmanagedType.Bool)> Boolean

    End Function
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def IsWow64Process(hHandle as int, ref is64Bits as bool) as bool:
     pass
```

## Notes:
```cs
Requires Windows XP SP2, Windows Vista, Windows Server 2003 SP1 or Windows Server 2008
```

## Tips & Tricks:
```cs
Use this instead of the processor architecture to determine if you are running on 64 bit.  You can use GetProcAddess to determine if your OS supports it (XP SP2 or greater).
```

## Sample Code:
```cs
isWow64 = false;
if ((System.Environment.OSVersion.Version.Major == 5 && System.Environment.OSVersion.Version.Minor >= 1) ||
      System.Environment.OSVersion.Version.Major > 5)
{
     SafeProcessHandle processHandle = GetProcessHandle((uint)System.Diagnostics.Process.GetCurrentProcess().Id);
     bool retVal;
     if (!NativeMethods.IsWow64Process(processHandle, out retVal))
     {
     throw new Win32Exception(Marshal.GetLastWin32Error());
     }
     isWow64 = retVal;
}
```

## Sample Code:
```cs
'Checks if the function exists on this OS, then calls it.
Private Shared Function IsWow64() As Boolean

    Dim proc As Integer
    proc = GetProcAddress(GetModuleHandle("Kernel32.dll"), "IsWow64Process")

    If proc <= 0 Then
        Return False
    End If
    'Dim processHandle As Long = GetProcessHandle(System.Diagnostics.Process.GetCurrentProcess().Id)
    Dim retVal As Boolean
    If IsWow64Process(GetCurrentProcess(), retVal) Then
        Return retVal
    Else
        Return False
    End If
End Function

'Uses Wow64 to see if the current process is running on Windows XP 64 bit
Public Shared Function IsWinXP64() As Boolean

    'returns True if running Windows XP 64-bit
    Dim osv As New OSVERSIONINFOEX

    osv.dwOSVersionInfoSize = Marshal.SizeOf(osv)

    Dim si As New SYSTEM_INFO

    If GetVersionEx(osv) = 1 Then

        GetSystemInfo(si)

        Return (osv.dwMajorVersion = 5 And osv.dwMinorVersion = 2) And _
             IsWow64()
    Else
        Return False
    End If
End Function

'Uses Wow64 to see if the current process is running on Windows Vista 64 bit
Public Shared Function IsWinVista64() As Boolean

    'returns True if running Windows Vista
    Dim osv As New OSVERSIONINFOEX

    osv.dwOSVersionInfoSize = Marshal.SizeOf(osv)

    If GetVersionEx(osv) = 1 Then

        Return (osv.wProductType = VER_NT_WORKSTATION) And _
             (osv.dwMajorVersion = 6) And IsWow64()
    Else
        Return False
    End If

End Function
```
