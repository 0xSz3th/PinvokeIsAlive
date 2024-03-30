
## C# Signature:
```cs
[return: MarshalAs(UnmanagedType.Bool)]
[DllImport("kernel32.dll", CharSet = CharSet.Auto, SetLastError = true)]
static extern bool GlobalMemoryStatusEx( [In,Out] MEMORYSTATUSEX lpBuffer); //Used to use ref with comment below
                                    // but ref doesn't work.(Use of [In, Out] instead of ref 
                                    //causes access violation exception on windows xp
                                    //comment: most probably caused by MEMORYSTATUSEX being declared as a class
                                    //(at least at pinvoke.net). On Win7, ref and struct work.

    // Alternate Version Using "ref," And Works With Alternate Code Below.
    // Also See Alternate Version Of [MEMORYSTATUSEX] Structure With
    // Fields Documented.
    [return: MarshalAs( UnmanagedType.Bool )]
    [DllImport( "kernel32.dll", CharSet = CharSet.Auto, EntryPoint = "GlobalMemoryStatusEx", SetLastError = true )]
    static extern bool _GlobalMemoryStatusEx( ref MEMORYSTATUSEX lpBuffer );
```

## VB.Net Signature:
```cs
Private Declare Function GlobalMemoryStatusEx Lib "kernel32" Alias "GlobalMemoryStatusEx" ( _
     <[In](), Out()>ByVal lpBuffer As MEMORYSTATUSEX _
     ) As <MarshalAs(UnmanagedType.Bool)> Boolean
```

## Sample Code:
```cs
{

            // Consumer of the NativeMethods class shown below

            long tm = System.GC.GetTotalMemory(true);

            NativeMethods oMemoryInfo = new NativeMethods();

            this.lblMemoryLoadNumber.Text = oMemoryInfo.MemoryLoad.ToString();
            this.lblIsMemoryTight.Text = oMemoryInfo.isMemoryTight().ToString();

            if (oMemoryInfo.isMemoryTight())
                this.lblIsMemoryTight.Text.Font.Bold = true;
            else
                this.lblIsMemoryTight.Text.Font.Bold = false;

        }
```

## Sample Code:
```cs
[CLSCompliant(false)]
    public class NativeMethods {

         private     MEMORYSTATUSEX msex;
         private uint _MemoryLoad;
         const int MEMORY_TIGHT_CONST = 80;

         public bool isMemoryTight()
          {
             if (_MemoryLoad > MEMORY_TIGHT_CONST )
                return true;
              else
                 return false;
         }

              public uint MemoryLoad
         {
            get { return _MemoryLoad; }
             internal set { _MemoryLoad = value; }
          }
```

## Sample Code:
```cs
public NativeMethods() {

            msex = new MEMORYSTATUSEX();
            if (GlobalMemoryStatusEx(msex)) {

                      _MemoryLoad = msex.dwMemoryLoad;
                 //etc.. Repeat for other structure members         

            }
                else
                 // Use a more appropriate Exception Type. 'Exception' should almost never be thrown
                 throw new Exception("Unable to initalize the GlobalMemoryStatusEx API");
        }

        [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
        private class MEMORYSTATUSEX
        {
                  public uint dwLength;
            public uint dwMemoryLoad;
                  public ulong ullTotalPhys;
                  public ulong ullAvailPhys;
                  public ulong ullTotalPageFile;
                  public ulong ullAvailPageFile;
                  public ulong ullTotalVirtual;
                  public ulong ullAvailVirtual;
                  public ulong ullAvailExtendedVirtual;
                  public MEMORYSTATUSEX()
            {
                      this.dwLength = (uint) Marshal.SizeOf(typeof( MEMORYSTATUSEX ));
            }
        }


         [return: MarshalAs(UnmanagedType.Bool)]
         [DllImport("kernel32.dll", CharSet = CharSet.Auto, SetLastError = true)]
         static extern bool GlobalMemoryStatusEx( [In, Out] MEMORYSTATUSEX lpBuffer);

    }
```

## Sample Code:
```cs
// Alternate Wrapper Method
    /// <summary>Retrieves information about the system's current usage of both physical and virtual memory.</summary>
    /// <param name="msex">Memory information structure that will be populated by this method</param>
    /// <returns>True if the wrapped native call was successfull, false if not.  Use 
    /// <see cref="Marshal.GetLastWin32Error"/> for additional error information</returns>
    public static bool GlobalMemoryStatus( ref MEMORYSTATUSEX msex )
    {
        msex.dwLength = (uint)Marshal.SizeOf( typeof( MEMORYSTATUSEX ) );

        return( _GlobalMemoryStatusEx( ref msex ) );
    }
```

## Alternative Managed API:
```cs
var info = new Microsoft.VisualBasic.Devices.ComputerInfo();
  Debug.WriteLine(info.TotalPhysicalMemory);
  Debug.WriteLine(info.AvailablePhysicalMemory);
  Debug.WriteLine(info.TotalVirtualMemory);
  Debug.WriteLine(info.AvailableVirtualMemory);
```
