
## C# Definition:
```cs
struct SOLE_AUTHENTICATION_SERVICE
{
   public int dwAuthnSvc;
   public int dwAuthzSvc;
   [MarshalAs(UnmanagedType.BStr)] public string pPrincipalName;
   public int hr;
}
```

## VB .NET Definition:
```cs
Structure SOLE_AUTHENTICATION_SERVICE
   Public dwAuthnSvc As Integer
   Public dwAuthzSvc As Integer
   <MarshalAs(UnmanagedType.BStr)> Public pPrincipalName As String
   Public hr As Integer
End Structure
```
