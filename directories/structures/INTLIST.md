
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct INTLIST 
{
    public int iValueCount;
    public int iValue1;
    public int iValue2;
    public int iValue3;
    public int iValue4;
    public int iValue5;
    public int iValue6;
    public int iValue7;
    public int iValue8;
    public int iValue9;
    public int iValue10;
}

[StructLayout(LayoutKind.Sequential)]
public struct INTLIST
{
     public int iValueCount;
     [MarshalAs(UnmanagedType.ByValArray, SizeConst=10)]
     public int[] iValues;
}
```

## VB .NET Signature:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure INTLIST
    Public iValueCount As Integer
    Public iValue1 As Integer
    Public iValue2 As Integer
    Public iValue3 As Integer
    Public iValue4 As Integer
    Public iValue5 As Integer
    Public iValue6 As Integer
    Public iValue7 As Integer
    Public iValue8 As Integer
    Public iValue9 As Integer
    Public iValue10 As Integer
End Structure

<StructLayout(LayoutKind.Sequential)> _
Public Structure INTLIST
    Public iValueCount As Integer
    <MarshalAs(UnmanagedType.ByValArray, SizeConst := 10)> _
    Public iValues As Integer()
End Structure

TODO
```
