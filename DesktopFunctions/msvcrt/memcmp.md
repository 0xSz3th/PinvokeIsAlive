
## C# Signature:
```cs
[DllImport("msvcrt.dll", CallingConvention=CallingConvention.Cdecl)]
static extern int memcmp(byte[] b1, byte[] b2, UIntPtr count);
```

## Sample Code:
```cs
//Extension Method example
public static class ByteArrayExtensions
{
   [DllImport("msvcrt.dll", CallingConvention=CallingConvention.Cdecl)]
   private static extern int memcmp(byte[] b1, byte[] b2, UIntPtr count);

   public static bool SequenceEqual(this byte[] b1, byte[] b2)
   {
      if (b1 == b2) return true; //reference equality check

      if (b1 == null || b2 == null || b1.Length != b2.Length) return false;

      return memcmp(b1, b2, new UIntPtr((uint)b1.Length)) == 0;
   }
}
```

## Edits:
```cs
Added (x86 and x64) signature and example. 
Removed SetLastError attribute from bottom 2 signatures as memset does not use this API.
Removed confusing signatures
```
