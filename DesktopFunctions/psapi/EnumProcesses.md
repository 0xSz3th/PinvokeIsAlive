
## C# Signature:
```cs
[DllImport("Psapi.dll", SetLastError=true)]
static extern bool EnumProcesses(
   [MarshalAs(UnmanagedType.LPArray, ArraySubType=UnmanagedType.U4)] [In][Out] UInt32[] processIds,
   UInt32 arraySizeBytes,
   [MarshalAs(UnmanagedType.U4)] out UInt32 bytesCopied
);
```

## VB Signature:
```cs
<DllImport("psapi.dll", CharSet:=CharSet.Auto, SetLastError:=True)> _
Public Shared Function EnumProcesses(<MarshalAs(UnmanagedType.LPArray, ArraySubType:=UnmanagedType.U4), [In](), [Out]()> ByVal processIds As Integer(), ByVal size As Integer, <[Out]()> ByRef needed As Integer) As Boolean
End Function
```

## Sample Code:
```cs
using System;
using System.Collections.Generic;
using System.Text;
using System.Runtime.InteropServices;

namespace Test
{
     class Program
     {
     [DllImport("psapi")]
     private static extern bool EnumProcesses(
         [MarshalAs(UnmanagedType.LPArray, ArraySubType = UnmanagedType.U4)] [In][Out] UInt32[] processIds,
           UInt32 arraySizeBytes,
           [MarshalAs(UnmanagedType.U4)] out UInt32 bytesCopied);

     static void Main(string[] args)
     {
         UInt32 arraySize = 120;
         UInt32 arrayBytesSize = arraySize * sizeof(UInt32);
         UInt32[] processIds = new UInt32[arraySize];
         UInt32 bytesCopied;

         bool success = EnumProcesses(processIds, arrayBytesSize, out bytesCopied);

         Console.WriteLine("success={0}", success);
         Console.WriteLine("bytesCopied={0}", bytesCopied);

         if (!success)
         {
         Console.WriteLine("Boo!");
         return;
         }
         if (0 == bytesCopied)
         {
         Console.WriteLine("Nobody home!");
         return;
         }

         UInt32 numIdsCopied = bytesCopied >> 2; ;

         if (0 != (bytesCopied & 3))
         {
         UInt32 partialDwordBytes = bytesCopied & 3;

         Console.WriteLine("EnumProcesses copied {0} and {1}/4th DWORDS...  Please ask it for the other {2}/4th DWORD",
             numIdsCopied, partialDwordBytes, 4 - partialDwordBytes);
         return;
         }

         for (UInt32 index = 0; index < numIdsCopied; index++)
         {
         Console.WriteLine("ProcessIds[{0}] = {1}", index, processIds[index]);
         }
     }
     }
}
```
