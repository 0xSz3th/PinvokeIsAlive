
## C# Signature:
```cs
[DllImport("msvcrt.dll", EntryPoint = "memcpy", CallingConvention = CallingConvention.Cdecl, SetLastError = false)]
public static extern IntPtr memcpy(IntPtr dest, IntPtr src, UIntPtr count);
```

## VB.NET Signature:
```cs
<DllImport("msvcrt.dll", EntryPoint:="memcpy", CallingConvention:=CallingConvention.Cdecl)> _
    Public Shared Sub CopyMemory(ByVal dest As IntPtr, ByVal src As IntPtr, ByVal count As Integer)
    End Sub
```

## VB Signature:
```cs
Declare Function memcpy Lib "msvcrt.dll" ( _
     ByVal dest As Any, _
     ByVal src As Any, _
     ByVal count As Long) _ 
     as Long
```

## Sample Code VB.Net:
```cs
Imports System.Runtime.InteropServices

    Sub Main()
    Dim managedArray1 As Char() = ("Ciao").ToCharArray
    Dim size As Integer = Marshal.SizeOf(managedArray1(0)) * managedArray1.Length
    Dim pnt1 As IntPtr = Marshal.AllocHGlobal(size)
    Dim pnt2 As IntPtr = Marshal.AllocHGlobal(size)
    Dim managedArray2(managedArray1.Length - 1) As Char
    Try
        Marshal.Copy(managedArray1, 0, pnt1, managedArray1.Length)
        '----MemCpy 
        CopyMemory(pnt2, pnt1, size * 2)
        '----
        Marshal.Copy(pnt2, managedArray2, 0, managedArray2.Length)
    Finally
        Marshal.FreeHGlobal(pnt1)
        Marshal.FreeHGlobal(pnt2)
    End Try
    Dim value As String = New String(managedArray2)
    Console.WriteLine(">>" + value + "<<")

    End Sub
```

## Sample Code C#:
```cs
public static Bitmap Clone(Bitmap src)
    {
        // get source image size
        int width = src.Width;
        int height = src.Height;

        // lock source bitmap data
        BitmapData srcData = src.LockBits(
        new Rectangle(0, 0, width, height),
        ImageLockMode.ReadWrite, src.PixelFormat);

        // create new image
        Bitmap dst = new Bitmap(width, height, src.PixelFormat);

        // lock destination bitmap data
        BitmapData dstData = dst.LockBits(
        new Rectangle(0, 0, width, height),
        ImageLockMode.ReadWrite, dst.PixelFormat);

        memcpy(dstData.Scan0, srcData.Scan0, new UIntPtr((uint)height * (uint)srcData.Stride));

        // unlock both images
        dst.UnlockBits(dstData);
        src.UnlockBits(srcData);        

        return dst;
    }
```
