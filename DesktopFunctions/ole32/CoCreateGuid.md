
## C# Signature:
```cs
[DllImport("ole32.dll", ExactSpelling=true, PreserveSig=false)]
static extern int CoCreateGuid ( out Guid guid );
```

## Sample Code:
```cs
Guid guid;
CoCreateGuid ( out guid );
string guid_s = guid.ToString();
// or:
Marshal.ThrowExceptionForHR ( CoCreateGuid ( out guid ) , new IntPtr ( -1 ) );
guid_s = guid.ToString();
```

## Alternative Managed API:
```cs
System.Guid.NewGuid()
```
