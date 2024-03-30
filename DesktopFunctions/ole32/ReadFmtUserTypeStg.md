
## C# Signature:
```cs
[DllImport("ole32.dll", CharSet=CharSet.Unicode, ExactSpelling=true, PreserveSig=false)]
static extern void ReadFmtUserTypeStg(IStorage pStg, out CLIPFORMAT pcf,
   [MarshalAs(UnmanagedType.LPWStr)] out string lplpszUserType);
```
