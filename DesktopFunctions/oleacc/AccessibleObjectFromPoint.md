
## C# Signature:
```cs
[DllImport("oleacc.dll")]
public static extern IntPtr AccessibleObjectFromPoint(POINT pt, [Out, MarshalAs(UnmanagedType.Interface)] out IAccessible accObj, [Out] out object ChildID);
```

## VB Signature:
```cs
<DllImport("oleacc.dll")> _
    Shared Function AccessibleObjectFromPoint(ByVal pt As Point, <MarshalAs(UnmanagedType.Interface)> ByRef accObj As IAccessible, ByRef ChildID As Object) As IntPtr
    End Function
```

## Sample Code:
```cs
public static IAccessible GetAccessibleObject(POINT pt, out int ChildID)
{
     object varChildID;
     IAccessible accObj;

     IntPtr success = AccessibleObjectFromPoint(pt, out accObj, out varChildID);
     ChildID = (int)varChildID;
     return accObj;
}
```
