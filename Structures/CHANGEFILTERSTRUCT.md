
## C# Definition:
```cs
/// <summary>
/// Contains extended result information obtained by calling the ChangeWindowMessageFilterEx function
/// </summary>
public struct CHANGEFILTERSTRUCT
{
     /// <summary>
     /// The size of the structure, in bytes. Must be set to sizeof(CHANGEFILTERSTRUCT)
     /// </summary>
     public UInt32 cbSize;
     /// <summary>
     /// If the function succeeds, this field contains a value from the ExtStatusEnum.
     /// </summary>
     public UInt32 ExtStatus;
}
```

## VB Definition:
```cs
Structure CHANGEFILTERSTRUCT 
   Public TODO
End Structure
```
