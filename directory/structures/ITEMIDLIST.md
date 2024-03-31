
## C# Definition:
```cs
/// <summary>
/// Contains a list of item identifiers.
/// </summary>
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
public struct ITEMIDLIST
{
      /// <summary>
      /// A list of item identifiers.
      /// </summary>
      [MarshalAs(UnmanagedType.Struct)]public SHITEMID mkid
  }
```

## VB.NET Definition:
```cs
''' <summary>
''' Contains a list of item identifiers.
''' </summary>
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Unicode)> _
Public Structure ITEMIDLIST
      ''' <summary>
      ''' A list of item identifiers.
      ''' </summary>
      <MarshalAs(UnmanagedType.Struct)>Public mkid As SHITEMID
End Structure
```

## VB Definition:
```cs
Public Type ITEMIDLIST   ' idl
    mkid As SHITEMID
End Type
```
