
## C# Signature:
```cs
[DllImport("gdi32.dll")]
public static extern bool SetDeviceGammaRamp(IntPtr hDC, ref RAMP lpRamp);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)] 
public struct RAMP
{
  [ MarshalAs(UnmanagedType.ByValArray, SizeConst=256)] 
  public UInt16[] Red;
  [ MarshalAs(UnmanagedType.ByValArray, SizeConst=256)] 
  public UInt16[] Green;
  [ MarshalAs(UnmanagedType.ByValArray, SizeConst=256)] 
  public UInt16[] Blue;
}
```

## Sample Code:
```cs
using System.Collections;
using System;
using System.Drawing;
using System.Runtime.InteropServices;
using System.Windows.Forms;
public class Test{

[DllImport("user32.dll")]
public static extern IntPtr GetDC(IntPtr hWnd);

[DllImport("gdi32.dll")]
public static extern bool SetDeviceGammaRamp(IntPtr hDC, ref RAMP lpRamp);

[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)] 
public struct RAMP
{
  [ MarshalAs(UnmanagedType.ByValArray, SizeConst=256)] 
  public UInt16[] Red;
  [ MarshalAs(UnmanagedType.ByValArray, SizeConst=256)] 
  public UInt16[] Green;
  [ MarshalAs(UnmanagedType.ByValArray, SizeConst=256)] 
  public UInt16[] Blue;
}

public static void SetGamma(int gamma)
{
  if (gamma <= 256 && gamma >= 1)
  {
   RAMP ramp = new RAMP();
   ramp.Red = new ushort[256];
   ramp.Green = new ushort[256];
   ramp.Blue = new ushort[256];
   for( int i=1; i<256; i++ )
   {
    int iArrayValue = i * (gamma + 128);

    if (iArrayValue > 65535)
    iArrayValue = 65535;
    ramp.Red[i] = ramp.Blue[i] = ramp.Green[i] = (ushort)iArrayValue;
   }
   SetDeviceGammaRamp(GetDC(IntPtr.Zero), ref ramp);
  }
  }

public static void Main(string[] args)
{
  string ent = "";
  int g=0;
  while (ent != "EXIT")
   {
    Console.WriteLine("Enter new Gamma (or 'EXIT' to quit):");
    ent = Console.ReadLine();
    try{
    g=int.Parse(ent);
    SetGamma(g);
    }
    catch{
    //Here only to catch errors where input is not a number (EXIT, for example, is a string)        
    }
   }
}
}
```
