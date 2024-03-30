
## C# Signature:
```cs
public delegate bool EnumWindowsProc(IntPtr hwnd, IntPtr lParam);

[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool EnumChildWindows(IntPtr hwndParent, EnumWindowsProc lpEnumFunc, IntPtr lParam);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", CharSet:=CharSet.Auto)> _
Private Shared Function EnumChildWindows(ByVal hWndParent As System.IntPtr, ByVal lpEnumFunc As EnumWindowsProc, ByVal lParam As Integer) As Boolean
End Function
```

## Sample Code (C#):
```cs
[DllImport("user32")]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool EnumChildWindows(IntPtr window, EnumWindowProc callback, IntPtr i);

/// <summary>
/// Returns a list of child windows
/// </summary>
/// <param name="parent">Parent of the windows to return</param>
/// <returns>List of child windows</returns>
public static List<IntPtr> GetChildWindows(IntPtr parent)
{
     List<IntPtr> result = new List<IntPtr>();
     GCHandle listHandle = GCHandle.Alloc(result);
     try
     {
     EnumWindowProc childProc = new EnumWindowProc(EnumWindow);
     EnumChildWindows(parent, childProc, GCHandle.ToIntPtr(listHandle));
     }
     finally
     {
     if (listHandle.IsAllocated)
         listHandle.Free();
     }
     return result;
}

/// <summary>
/// Callback method to be used when enumerating windows.
/// </summary>
/// <param name="handle">Handle of the next window</param>
/// <param name="pointer">Pointer to a GCHandle that holds a reference to the list to fill</param>
/// <returns>True to continue the enumeration, false to bail</returns>
private static bool EnumWindow(IntPtr handle, IntPtr pointer)
{
     GCHandle gch = GCHandle.FromIntPtr(pointer);
     List<IntPtr> list = gch.Target as List<IntPtr>;
     if (list == null)
     {
     throw new InvalidCastException("GCHandle Target could not be cast as List<IntPtr>");
     }
     list.Add(handle);
     //  You can modify this to check to see if you want to cancel the operation, then return a null here
     return true;
}

/// <summary>
/// Delegate for the EnumChildWindows method
/// </summary>
/// <param name="hWnd">Window handle</param>
/// <param name="parameter">Caller-defined variable; we use it for a pointer to our list</param>
/// <returns>True to continue enumerating, false to bail.</returns>
public delegate bool EnumWindowProc(IntPtr hWnd, IntPtr parameter);
```

## Sample Code 2 (C#):
```cs
private static ArrayList GetAllWindows()
{
    var windowHandles = new ArrayList();
    EnumedWindow callBackPtr = GetWindowHandle;
    EnumWindows(callBackPtr, windowHandles);

    foreach (IntPtr windowHandle in windowHandles.ToArray())
    {
       EnumChildWindows(windowHandle, callBackPtr, windowHandles);
    }

    return windowHandles;
}

private delegate bool EnumedWindow(IntPtr handleWindow, ArrayList handles);

[DllImport("user32.dll", CharSet = CharSet.Auto, SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
private static extern bool EnumWindows(EnumedWindow lpEnumFunc, ArrayList lParam);

[DllImport("user32")]
[return: MarshalAs(UnmanagedType.Bool)]
private static extern bool EnumChildWindows(IntPtr window, EnumedWindow callback, ArrayList lParam);

private static bool GetWindowHandle(IntPtr windowHandle, ArrayList windowHandles)
{
    windowHandles.Add(windowHandle);
    return true;
}
```

## Sample Code (VB.net):
```cs
Imports System.Runtime.InteropServices
Public Class NativeMethods
     <DllImport("User32.dll")> _
     Private Shared Function EnumChildWindows _
     (ByVal WindowHandle As IntPtr, ByVal Callback As EnumWindowProcess, _
     ByVal lParam As IntPtr) As Boolean
     End Function

     Public Delegate Function EnumWindowProcess(ByVal Handle As IntPtr, ByVal Parameter As IntPtr) As Boolean

     Public Shared Function GetChildWindows(ByVal ParentHandle As IntPtr) As IntPtr()
     Dim ChildrenList As New List(Of IntPtr)
     Dim ListHandle As GCHandle = GCHandle.Alloc(ChildrenList)
     Try
         EnumChildWindows(ParentHandle, AddressOf EnumWindow, GCHandle.ToIntPtr(ListHandle))
     Finally
         If ListHandle.IsAllocated Then ListHandle.Free()
     End Try
     Return ChildrenList.ToArray
     End Function

     Private Shared Function EnumWindow(ByVal Handle As IntPtr, ByVal Parameter As IntPtr) As Boolean
     Dim ChildrenList As List(Of IntPtr) = GCHandle.FromIntPtr(Parameter).Target
     If ChildrenList Is Nothing Then Throw New Exception("GCHandle Target could not be cast as List(Of IntPtr)")
     ChildrenList.Add(Handle)
     Return True
     End Function
End Class
```
