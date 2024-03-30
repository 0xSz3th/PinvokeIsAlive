
## C# Signature:
```cs
[DllImport("ntdll.dll")]
public static extern int NtQuerySymbolicLinkObject(
   SafeFileHandle LinkHandle,
   ref UNICODE_STRING LinkTarget,
   out int ReturnedLength);
```

## Tips & Tricks:
```cs
int len;
var buffer = new UNICODE_STRING(new string(' ', 512));
NtQuerySymbolicLinkObject(h, ref buffer, out len);
Debug.WriteLine(buffer.ToString());
```
