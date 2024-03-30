
## C# Signature:
```cs
[DllImport("oleacc.dll")]
public static extern uint WindowFromAccessibleObject(IAccessible pacc, ref IntPtr phwnd );
```

## VB .NET Signature:
```cs
Declare Function WindowFromAccessibleObject Lib "oleacc.dll" (ByVal pacc as IAccessible, ByRef phwnd as IntPtr) As Integer
```

## Sample Code c#:
```cs
//MouseHook.POINT structure type of POINT 
    public class Miscelanious
    {
    static Accessibility.IAccessible iAccessible;//interface: Accessibility namespace
    static object ChildId;
    public static IntPtr GetControlHandlerFromPoint(MouseHook.POINT location)
    {
        IntPtr handler=IntPtr.Zero;

        handler = AccessibleObjectFromPoint(location,out iAccessible,out ChildId);
        WindowFromAccessibleObject(iAccessible, ref handler);
        return handler;

    }
    public static string GetText()
    {
        if (iAccessible != null && ChildId != null)
        {
        return iAccessible.get_accName(ChildId);
        }
        else return "none";

    }


    #region DLLIMPORT

    [DllImport("oleacc.dll")]
    public static extern IntPtr AccessibleObjectFromPoint(MouseHook.POINT pt, [Out, MarshalAs(UnmanagedType.Interface)] out IAccessible accObj, [Out] out object ChildID);

    [DllImport("oleacc.dll")]
    public static extern uint WindowFromAccessibleObject(IAccessible pacc, ref IntPtr phwnd);
    #endregion
    }
```
