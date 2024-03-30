
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern int MultiByteToWideChar(uint CodePage, uint dwFlags, string
   lpMultiByteStr, int cbMultiByte, [Out, MarshalAs(UnmanagedType.LPWStr)]
   StringBuilder lpWideCharStr, int cchWideChar);
```

## C# Signature:
```cs
[DllImport("kernel32.dll")]
    private static extern int MultiByteToWideChar(
      uint CodePage, 
      uint dwFlags,
      [MarshalAs(UnmanagedType.LPArray)] Byte[] lpMultiByteStr,
      int cbMultiByte,
      [Out, MarshalAs(UnmanagedType.LPArray)]
      Byte[] lpWideCharStr, 
      int cchWideChar);
```

## Sample Code:
```cs
[DllImport("kernel32.dll")]
  private static extern int MultiByteToWideChar(
    uint CodePage,
    uint dwFlags,
    [MarshalAs(UnmanagedType.LPArray)] Byte[] lpMultiByteStr,
    int cbMultiByte,
    [Out, MarshalAs(UnmanagedType.LPArray)]
      Byte[] lpWideCharStr,
    int cchWideChar);

  [SqlFunction]
  public static SqlString ConvToUnicode(SqlInt32 codepage, SqlString multibyteString) {
    bool un;
    byte[] b = (byte[])iConvToMultibyteArray(multibyteString, out un);
    if (un) return (SqlString)ToUnicode((uint)(int)codepage, b);
    else return multibyteString;
  }

  private static SqlBinary iConvToMultibyteArray(SqlString multibyteString, out bool multibyte) {
    byte[] result;
    byte[] ch = multibyteString.GetUnicodeBytes();
    if ((ch.Length >= 2) && (ch[1] == 0x00)) {
      result = new byte[ch.Length / 2];
      for (int i = 0; i < ch.Length / 2; i++) {
    result[i] = ch[i * 2];
      }
      multibyte = true;
    }
    else {
      result = ch;// new byte[ch.Length];
      multibyte = false;
    }
    return (SqlBinary)result;
  }
```
