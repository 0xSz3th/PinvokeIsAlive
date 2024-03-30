
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet=CharSet.Auto)]
static extern IntPtr lstrcpy(
    [Out] StringBuilder lpString1, 
    string lpString2);
```

## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet=CharSet.Auto)]
static extern IntPtr lstrcpy(
    [Out] IntPtr lpString1, 
    string lpString2);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", CharSet:=CharSet.Auto)> _
   Private Shared Function lstrcpy(<Out> lpString1 As StringBuilder, lpString2 As String) As IntPtr
End Function
```
