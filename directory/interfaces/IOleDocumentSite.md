
## C# Definition:
```cs
[ComImport]
[Guid("b722bcc7-4e68-101b-a2bc-00aa00404770")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IOleDocumentSite
{
     void ActivateMe(ref object pViewToActivate);
}
```

## VB Definition:
```cs
<ComImport(), _
  Guid("b722bcc7-4e68-101b-a2bc-00aa00404770"), _
  InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ 
Public Interface IOleDocumentSite
   Sub ActivateMe(ByRef pViewToActivate As Object)
End Interface
```
