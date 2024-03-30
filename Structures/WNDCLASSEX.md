
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
public struct WNDCLASSEX
{
    [MarshalAs(UnmanagedType.U4)]
    public int cbSize;
    [MarshalAs(UnmanagedType.U4)]
    public int style;
    public IntPtr lpfnWndProc; // not WndProc
    public int cbClsExtra;
    public int cbWndExtra;
    public IntPtr hInstance;
    public IntPtr hIcon;
    public IntPtr hCursor;
    public IntPtr hbrBackground;
    public string lpszMenuName;
    public string lpszClassName;
    public IntPtr hIconSm;  

    //Use this function to make a new one with cbSize already filled in.
    //For example:
    //var WndClss = WNDCLASSEX.Build()
    public static WNDCLASSEX Build()
    {
    var nw = new WNDCLASSEX();
    nw.cbSize = Marshal.SizeOf(typeof (WNDCLASSEX));
    return nw;
    }
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Structure WNDCLASSEX
   Public cbSize As UInteger
   Public style As ClassStyles
   <MarshalAs(UnmanagedType.FunctionPtr)>
   Public lpfnWndProc As IntPtr
   Public cbClsExtra As Integer
   Public cbWndExtra As Integer
   Public hInstance As IntPtr
   Public hIcon As IntPtr
   Public hCursor As IntPtr
   Public hbrBackground As IntPtr
   Public lpszMenuName As String
   Public lpszClassName As String
   Public hIconSm As IntPtr

   ' Use this function to make a new one with cbSize already filled in.
   ' For example:
   'Dim WndClss As WNDCLASSEX = WNDCLASSEX.GetNew()
   Shared Function MakeNew()
      Dim nw as New WNDCLASSEX
      nw.cbSize=Marshal.SizeOf(GetType(WNDCLASSEX))
      return nw
   End Function
End Structure
```

## IMPORTANT:
```cs
<MarshalAs(UnmanagedType.LPTStr)> _
Public lpszMenuName As String
<MarshalAs(UnmanagedType.LPTStr)> _
Public lpszClassName As String
```
