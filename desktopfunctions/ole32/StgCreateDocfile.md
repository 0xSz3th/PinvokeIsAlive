
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int StgCreateDocfile([MarshalAs(UnmanagedType.LPWStr)]
   string pwcsName, STGM grfMode, uint reserved, out IStorage ppstgOpen);
```
