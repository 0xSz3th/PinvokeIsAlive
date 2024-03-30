
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern int SHQueryRecycleBin(string pszRootPath, ref SHQUERYRBINFO
   pSHQueryRBInfo);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, Pack=4)]
public struct SHQUERYRBINFO
{
    public int  cbSize;
    public long i64Size;
    public long i64NumItems;
}
```

## Sample Code:
```cs
public static int GetCount()
{
    SHQUERYRBINFO sqrbi = new SHQUERYRBINFO();
    sqrbi.cbSize = Marshal.SizeOf(typeof(SHQUERYRBINFO));
    int hresult = SHQueryRecycleBin(string.Empty, ref sqrbi);
    return (int)sqrbi.i64NumItems;
}
```

##  N.B.
```cs
int hresult = SHQueryRecycleBin(@"C:\", ref sqrbi);
```
