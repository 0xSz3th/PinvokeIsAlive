
## C# Definition:
```cs
using System.Runtime.InteropServices;

[StructLayout(LayoutKind.Sequential, Pack=2)]
public struct BITMAPFILEHEADER
{
     public ushort bfType; 
     public uint bfSize; 
     public ushort bfReserved1; 
     public ushort bfReserved2; 
     public uint bfOffBits; 
}
```

## VB Definition:
```cs
Imports System.Runtime.InteropServices

<StructLayout(LayoutKind.Sequential, Pack:=2)> _
Structure BITMAPFILEHEADER 
   Public Type As UShort
   Public Size As UInteger
   Public Reserved1 As UShort
   Public Reserved2 As UShort
   Public OffBits As UInteger
End Structure
```
