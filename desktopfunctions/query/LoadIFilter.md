
## C# Signature:
```cs
[DllImport("query.dll", SetLastError=true, CharSet=CharSet.Unicode)]
static extern int LoadIFilter(string pwcsPath,
          [MarshalAs(UnmanagedType.IUnknown)] object pUnkOuter,
          ref IFilter ppIUnk);
```

## VB Signature:
```cs
Declare Unicode Function LoadIFilter Lib "query.dll" (ByVal pwcsPath As String, _
           <MarshalAs(UnmanagedType.IUnknown)> ByVal pUnkOuter As Object, _
                               ByRef ppIUnk As IFilter) As Integer
```
