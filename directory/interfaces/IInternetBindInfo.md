
## C# Definition:
```cs
[ComImport]
[Guid("79EAC9E1-BAF9-11CE-8C82-00AA004BA90B"), InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IInternetBindInfo
{
    void GetBindInfo(out uint grfBINDF, [In, Out] ref BINDINFO pbindinfo);
    void GetBindString(uint ulStringType, [MarshalAs(UnmanagedType.LPWStr)] ref string ppwzStr, uint cEl, ref uint pcElFetched);
}
```

## VB Definition:
```cs
<ComImport> _
<Guid("79EAC9E1-BAF9-11CE-8C82-00AA004BA90B"), InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
```

## VB Definition:
```cs
Sub GetBindInfo(<Out()> ByRef grfBINDF As UInt32, <[In](), Out()> ByRef pbindinfo As BINDINFO)
    Sub GetBindString(ByVal ulStringType As UInt32, <MarshalAs(UnmanagedType.LPWStr)> ByRef ppwzStr As String, ByVal cEl As UInt32, ByRef pcElFetched As UInt32)
```
