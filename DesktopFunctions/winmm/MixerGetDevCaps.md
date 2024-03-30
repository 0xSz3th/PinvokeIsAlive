
## C# Signature:
```cs
[DllImport("winmm.dll", EntryPoint="mixerGetDevCaps", SetLastError=true)]
   private static extern uint MixerGetDevCaps(int mixerId, ref MixerCaps mixerCaps, int mixerCapsSize);
```

## VB Signature:
```cs
<DllImport("winmm.dll", EntryPoint:="mixerGetDevCaps", SetLastError:=True)> _
   Private Shared Function MixerGetDevCaps(ByVal mixerId As Integer, ByRef mixerCaps As MixerCaps, ByVal mixerCapsSize As Integer) As UInteger
   End Function
```

## Sample Code:
```cs
using System;
   using System.Runtime.InteropServices;

   namespace ConsoleApplication3
   {
       class Program
       {
       [DllImport("winmm.dll", EntryPoint = "mixerGetNumDevs")]
       private static extern uint MixerGetNumDevs();

       [DllImport("winmm.dll", EntryPoint = "mixerGetDevCaps", SetLastError = true)]
       private static extern uint MixerGetDevCaps(int mixerId, ref MixerCaps mixerCaps, int mixerCapsSize);

       [StructLayout(LayoutKind.Sequential)]
       struct MixerCaps
       {
           public ushort ManufacturerID;
           public ushort ProductId;
           public int Version;
           [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
           public String ProductName;
           public uint Support;
           public uint Destinations;
           public override String ToString()
           {
           return String.Format("Manufacturer ID: {0}, Product ID: {1}, Driver Version: {2}, Product Name: \"{3}\", Support: {4}, Destinations: {5}", ManufacturerID, ProductId, Version, ProductName, Support, Destinations);
           }
       }

       static void Main(string[] args)
       {
           uint numDevs = MixerGetNumDevs();            
           for (int mixerId = 0; mixerId < numDevs; mixerId++)
           {
           MixerCaps caps = new MixerCaps();
           uint result = MixerGetDevCaps(mixerId, ref caps, Marshal.SizeOf(caps));
           Console.WriteLine(caps.ToString());        
           }
           Console.ReadKey();
       } 
       }
   }
```
