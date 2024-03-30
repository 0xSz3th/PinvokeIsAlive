
## C# Signature:
```cs
//hint: nint - platform specific int for pointers (Int32 for x86 or Long for x64)
[DllImport("kernel32.dll")]
static extern bool SetProcessWorkingSetSize(IntPtr hProcess, nint dwMinimumWorkingSetSize, nint dwMaximumWorkingSetSize);
```

## VB.NET Signature:
```cs
'for x86
     Private Declare Function SetProcessWorkingSetSize Lib "kernel32.dll" (ByVal hProcess As IntPtr, ByVal dwMinimumWorkingSetSize As Int32, ByVal dwMaximumWorkingSetSize As Int32) As Int32

     'for x64
     Private Declare Function SetProcessWorkingSetSize Lib "kernel32.dll" (ByVal hProcess As IntPtr, ByVal dwMinimumWorkingSetSize As Long, ByVal dwMaximumWorkingSetSize As Long) As Int32
```

## C#
```cs
public class MemoryManagement{

        [DllImport("kernel32.dll")]
        public static extern bool SetProcessWorkingSetSize( IntPtr proc, nint min, nint max );

        public void FlushMemory() {
            GC.Collect() ;
            GC.WaitForPendingFinalizers() ;
            if(Environment.OSVersion.Platform == PlatformID.Win32NT) {
                SetProcessWorkingSetSize(System.Diagnostics.Process.GetCurrentProcess().Handle, -1, -1) ;
            }
        }
   }
```

## VB.NET
```cs
Friend Sub ReleaseMemory()
      Try
           GC.Collect()
           GC.WaitForPendingFinalizers()
           If Environment.OSVersion.Platform = PlatformID.Win32NT Then
            SetProcessWorkingSetSize(System.Diagnostics.Process.GetCurrentProcess().Handle, -1, -1)
           End If
      Catch
      End Try
     End Sub
```
