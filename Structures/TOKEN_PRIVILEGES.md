
## C# Definition:
```cs
struct TOKEN_PRIVILEGES {
   public int PrivilegeCount;
   [MarshalAs(UnmanagedType.ByValArray, SizeConst=ANYSIZE_ARRAY)]
   public LUID_AND_ATTRIBUTES [] Privileges;
}
```

## VB Definition:
```cs
Public Const ANYSIZE_ARRAY As Integer = 1
<StructLayout(LayoutKind.Sequential)> _
Public Structure TOKEN_PRIVILEGES
   Public PrivilegeCount As UInt32
   <MarshalAs(UnmanagedType.ByValArray, SizeConst:=ANYSIZE_ARRAY)> _
   Public Privileges() As LUID_AND_ATTRIBUTES
End Structure
```
