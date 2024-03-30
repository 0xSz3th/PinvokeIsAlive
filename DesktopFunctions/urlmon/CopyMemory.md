
## VB Signature:
```cs
Public Declare Auto Sub CopyMemory lib "kernel32.dll" Alias "CopyMemory"(destination As IntPtr, source As IntPtr, length As UInteger)

<DllImport("kernel32.dll", SetLastError:= True, EntryPoint:= "CopyMemory")>
Public Shared Sub CopyMemory(destination As IntPtr, source As IntPtr, length As UInteger)
End Sub
```

## Sample Code:
```cs
// static void Main()
    // {
    //   const int size = 200;
    //   IntPtr memorySource = Marshal.AllocHGlobal(size);
    //   IntPtr memoryTarget = Marshal.AllocHGlobal(size);
    //   CopyMemory(memoryTarget,memorySource,size);
    // }

     [DllImport("kernel32.dll", SetLastError=true, EntryPoint="CopyMemory")
     public static void CopyMemory(void* destination, void* source, uint length);

     public static unsafe void Main()
      {
     int[] data = Enumerable.Range(1, 1000000);
     int size = data.Length * sizeof(int);
     byte[] dst = new byte[size]
     fixed (byte* pd = dst){ fixed(int* ps = data){ CopyMemory(pd, ps, size); } }
     Console.WriteLine("10 data result : {0}", BitConverter.ToString(dst, 0, 10));
     Console.WriteLine("Is assuming equals : {0}", BitConverter.ToInt32(dst, 0) == data[0] && 
                               BitConverter.ToInt32(dst, dst.GetUpperBound(0) - sizeof(int)) == data[data.GetUpperBound(0)]);
     Console.ReadKey();
      }
```

## Sample Code VB:
```cs
Public Module CopyMemoryTest

      Public Declare Auto Sub CopyMemory lib "kernel32.dll" Alias "CopyMemory"(destination As IntPtr, source As IntPtr, length As UInteger)

      Public Sub Main(ParamArray args As String())
    Dim source As Byte() = File.ReadAllBytes("C:\Windows\explorer.exe"),
        destination(source.GetUpperBound(0)) As Byte,
        length As UInteger = CUInt(source.Length),
        sourcePtr As IntPtr = Marshal.UnsafeAddrOfPinnedArrayElement(source, 0),
        targetPtr As IntPtr = Marshal.UnsafeAddrOfPinnedArrayElement(target, 0)
    Dim sw As Stopwatch = Stopwatch.StartNew()
    CopyMemory(targetPtr, sourcePtr, length)
    sw.Stop()
    Console.WriteLine("Total time to copy {0:N0} bytes = {1}", new TimeSpan(sw.ElapsedTicks))
    Using sha = New System.Security.Cryptography.SHA512Managed
      Dim sourceChecksum = sha.ComputeHash(source), 
          destinationCheksum = sha.ComputeHash(destination), 
          isEquals = True
      For i = 0 To sourceChecksum.GetUpperBound(0)
        If sourceChecksum(i) <> destinationChecksum(i) Then
           Console.WriteLine("The copy memory is bad, some of data are not copied..")
           IsEquals = False
           Exit For
        End If
      Next i
      If isEquals Then Console.WriteLine("The copy memory is perfectly copy all bytes.")
    End Using 
    Console.ReadKey().Key = ConsoleKeys.R Then
       Main(args)
    End If
    sw = Nothing
    Erase source, destination
      End Sub

   End Module
```
