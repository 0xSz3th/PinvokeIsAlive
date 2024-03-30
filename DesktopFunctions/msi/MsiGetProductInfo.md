
## C# Signature:
```cs
[DllImport("msi.dll", CharSet=CharSet.Unicode)]
static extern Int32 MsiGetProductInfo(string product, string property, [Out] StringBuilder valueBuf, ref Int32 len);
```

## VB Signature:
```cs
Declare Auto Function MsiGetProductInfo Lib "msi.dll" (ByVal product As String, ByVal [property] As String, <MarshalAs(UnmanagedType.VBByRefStr)> ByRef valueBuf As String, ByRef len As Long) As Int32
```

## Sample Code:
```cs
Int32 len = 512;
System.Text.StringBuilder builder = new System.Text.StringBuilder(len);
MsiGetProductInfo("{4B3334CE-06D9-4446-BBC5-EB4C9D75BFF6}", "InstallSource", builder , ref len);
return builder.ToString(0, len);
```

## VB Sample:
```cs
result = New String(" ", 255)
len = 255
MsiGetProductInfo("{4B3334CE-06D9-4446-BBC5-EB4C9D75BFF6}", "InstallSource", result, len)
result = left$(result,len)
```
