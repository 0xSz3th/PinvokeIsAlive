
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet=CharSet.Auto)]
static extern IntPtr lstrcpyn(
    [Out] StringBuilder lpString1, 
    string lpString2,
    int iMaxLength);
```

## Sample Code:
```cs
[DllImport("kernel32", CharSet = CharSet.Auto)]
static extern IntPtr lstrcpyn(IntPtr dest, IntPtr src, int len);

void FillABuffer(IntPtr dest, int dest_maxlen, string source)
{
   IntPtr tmp_ptr = Marshal.StringToHGlobalAuto(source);
   lstrcpyn(dest, tmp_ptr, dest_maxlen);
   Marshal.FreeHGlobal(tmp_ptr);
}
```
