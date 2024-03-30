
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
  public struct APPBARDATA
  {
    public int cbSize; // initialize this field using: Marshal.SizeOf(typeof(APPBARDATA));
    public IntPtr hWnd;
    public uint uCallbackMessage;
    public uint uEdge;
    public RECT rc;
    public int lParam;
  }
```

## VB Signature:
```cs
<StructLayout(LayoutKind.Sequential)> Structure APPBARDATA
    Public cbSize As Integer
    Public hWnd As IntPtr
    Public uCallbackMessage As Integer
    Public uEdge As Integer
    Public rc As RECT
    Public lParam As IntPtr
  End Structure
```

## Tips & Tricks:
```cs
[StructLayout(LayoutKind.Sequential)]
  public struct APPBARDATA
  {
    public int cbSize; // initialize this field using: Marshal.SizeOf(typeof(APPBARDATA));
    public IntPtr hWnd;
    public uint uCallbackMessage;
    public uint uEdge;
    public RECT rc;
    public int lParam;
    public static APPBARDATA NewAPPBARDATA()
    {
      APPBARDATA abd = new APPBARDATA();
      abd.cbSize = Marshal.SizeOf(typeof(APPBARDATA));
      return abd;
    }
  }

  ...
  APPBARDATA myBarData = APPBARDATA.NewAPPBARDATA();
  myBarData.hWnd = MyBar.Handle;
  ...
```
