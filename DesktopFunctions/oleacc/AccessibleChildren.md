
## C# Signature:
```cs
[DllImport("oleacc.dll")]
public static extern uint AccessibleChildren( IAccessible paccContainer, int iChildStart, int cChildren, [Out] object[] rgvarChildren, out int pcObtained);
```

## VB .NET Signature:
```cs
Declare Function AccessibleChildren Lib "oleacc.dll" (ByVal paccContainer As IAccessible, ByVal iChildStart As Integer, ByVal cChildren As Integer, <[Out]()> ByVal rgvarChildren() As Object, ByRef pcObtained As Integer) As UInteger
```

## VB .NET Signature:
```cs
<DllImport("oleacc.dll")> _
Function AccessibleChildren(ByVal paccContainer As IAccessible, ByVal iChildStart As Integer, ByVal cChildren As Integer, <[Out]()> ByVal rgvarChildren() As Object, ByRef pcObtained As Integer) As UInteger
End Function
```
