
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int StgOpenStorageOnILockBytes(ILockBytes plkbyt,
   IStorage pStgPriority, uint grfMode, IntPtr snbEnclude, uint reserved,
   out IStorage ppstgOpen);
```
