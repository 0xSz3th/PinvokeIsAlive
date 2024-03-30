
## C# Definition:
```cs
struct NAME_BUFFER {
   public TODO;
}
```

## VB Definition:
```cs
Private Const NCBNAMSZ As Integer = 16

<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Ansi)> _
Private Structure NAME_BUFFER
   <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=NCBNAMSZ)> Dim Name As String
   Dim name_num As Byte
   Dim name_flags As Byte
End Structure
```

## Notes:
```cs
typedef struct _NAME_BUFFER { 
   UCHAR name[NCBNAMSZ]; 
   UCHAR name_num; 
   UCHAR name_flags; 
} NAME_BUFFER, *PNAME_BUFFER;
```
