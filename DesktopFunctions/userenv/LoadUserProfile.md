
## C# Signature:
```cs
[DllImport("userenv.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern bool LoadUserProfile(IntPtr hToken, ref PROFILEINFO lpProfileInfo);
```

## VB Signature:
```cs
<DllImport("userenv.dll", EntryPoint:="LoadUserProfile", SetLastError:=True, CharSet:=CharSet.Auto)> _
        Public Shared Function LoadUserProfile(ByVal hToken As IntPtr, ByRef lpProfileInfo As PROFILEINFO) As Boolean
    End Function
```
