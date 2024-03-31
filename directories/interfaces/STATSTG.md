
## C# Definition:	
```cs
public struct STATSTG
{
      [MarshalAs(UnmanagedType.LPTStr)]     
      public string pwcsName;
      public int type;
      public long cbSize;
      public FILETIME mtime;
      public FILETIME ctime;
      public FILETIME atime;
      public int grfMode;
      public int grfLocksSupported;
      public Guid clsid;
      public int grfStateBits;
      public int reserved;
}
```
