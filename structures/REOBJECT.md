
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
class REOBJECT {
  public int cbStruct = Marshal.SizeOf(typeof(REOBJECT));
  public int cp;
  public Guid clsid;
  public IOleObject poleobj;
  public IStorage pstg;
  public IOleClientSite polesite;
  public Size sizel;
  public uint dvAspect;
  public uint dwFlags;
  public uint dwUser;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Class REOBJECT 
   Public TODO
End Structure
```

## Notes:
```cs
DWORD cbStruct;
    LONG cp;
    CLSID clsid;
    LPOLEOBJECT poleobj;
    LPSTORAGE pstg;
    LPOLECLIENTSITE polesite;
    SIZEL sizel;
    DWORD dvaspect;
    DWORD dwFlags;
    DWORD dwUser;
```
