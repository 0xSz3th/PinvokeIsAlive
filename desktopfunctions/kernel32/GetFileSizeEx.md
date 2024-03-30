
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool GetFileSizeEx(IntPtr hFile, out long lpFileSize);
```

## VB.Net Signature:
```cs
<DllImport("kernel32.dll",CharSet:=CharSet.Auto)> _
Public Shared Function GetFileSizeEx( _
                <[In]()> ByVal hFile As IntPtr, _
                <[In](), Out()> ByRef lpFileSize As Long) As Boolean
```

## Sample Code:
```cs
IntPtr handle = CreateFile(PathString, GENERIC_READ, FILE_SHARE_READ, 0, OPEN_EXISTING, FILE_ATTRIBUTE_READONLY, 0); //PInvoked too
        if (handle.ToInt32() == -1) 
        {
        return; 
        }
        long fileSize;
        bool result = GetFileSizeEx(handle, out fileSize);
        if (!result) 
        {
        return;
        }
```
