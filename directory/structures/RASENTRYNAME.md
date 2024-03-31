
## C# Definition:
```cs
struct RASENTRYNAME 
{ 
    public int  dwSize; 
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst=256 + 1)]
    public string szEntryName;         
    public int dwFlags;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst=260 + 1)]
    public string szPhonebookPath;
}
```

## VB Definition:
```cs
Structure RASENTRYNAME 
   Public TODO
End Structure
```
