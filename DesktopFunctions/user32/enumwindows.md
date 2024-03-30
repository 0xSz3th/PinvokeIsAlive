
## C# Signature:
```cs
[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool EnumWindows(EnumWindowsProc lpEnumFunc, IntPtr lParam);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
Private Shared Function EnumWindows(
ByVal lpEnumFunc As EnumWindowsProc, _
ByVal lParam As IntPtr) As Boolean
End Function
```

## Tips & Tricks:
```cs
using System.Runtime.InteropServices;

public delegate bool CallBackPtr(int hwnd, int lParam);
private CallBackPtr callBackPtr;

public class EnumReport 
{
    [DllImport("user32.dll")]
    private static extern int EnumWindows(CallBackPtr callPtr, int lPar); 

    public static bool Report(int hwnd, int lParam) 
    { 
        Console.WriteLine("Window handle is "+hwnd);
        return true;
    }
}
static void Main()
{

     // note in other situations, it is important to keep 
     // callBackPtr as a member variable so it doesnt GC while you're calling EnumWindows

     callBackPtr = new CallBackPtr(EnumReport.Report);  
    EnumReport.EnumWindows(callBackPtr, 0);
}
```

## Tips & Tricks:
```cs
public delegate bool EnumedWindow(IntPtr handleWindow, ArrayList handles);

      [DllImport("user32.dll", CharSet = CharSet.Auto, SetLastError = true)]
      [return: MarshalAs(UnmanagedType.Bool)]
      public static extern bool EnumWindows(EnumedWindow lpEnumFunc, ArrayList lParam);

      public static ArrayList GetWindows()
      {    
     ArrayList windowHandles = new ArrayList();
     EnumedWindow callBackPtr = GetWindowHandle;
     EnumWindows(callBackPtr, windowHandles);

        return windowHandles;     
      }

      private static bool GetWindowHandle(IntPtr windowHandle, ArrayList windowHandles)
      {
     windowHandles.Add(windowHandle);
     return true;
      }
```

## Tips & Tricks:
```cs
using System.Runtime.InteropServices;
using System.Text;

public class WndSearcher
{
    public static IntPtr SearchForWindow(string wndclass, string title)
    {
        SearchData sd = new SearchData { Wndclass=wndclass, Title=title };
        EnumWindows(new EnumWindowsProc(EnumProc), ref sd);
        return sd.hWnd;
    }

    public static bool EnumProc(IntPtr hWnd, ref SearchData data)
    {
        // Check classname and title 
        // This is different from FindWindow() in that the code below allows partial matches
        StringBuilder sb = new StringBuilder(1024);
        GetClassName(hWnd, sb, sb.Capacity);
        if (sb.ToString().StartsWith(data.Wndclass))
        {
            sb = new StringBuilder(1024);
            GetWindowText(hWnd, sb, sb.Capacity);
            if (sb.ToString().StartsWith(data.Title))
            {
                data.hWnd = hWnd;
                return false;    // Found the wnd, halt enumeration
            }
        }
        return true;
    }

    public class SearchData
    {
        // You can put any dicks or Doms in here...
        public string Wndclass;
        public string Title;
        public IntPtr hWnd;
    } 

    private delegate bool EnumWindowsProc(IntPtr hWnd, ref SearchData data);

    [DllImport("user32.dll")]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern bool EnumWindows(EnumWindowsProc lpEnumFunc, ref SearchData data);

    [DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    public static extern int GetClassName(IntPtr hWnd, StringBuilder lpClassName, int nMaxCount);

    [DllImport("user32.dll", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern int GetWindowText(IntPtr hWnd, StringBuilder lpString, int nMaxCount);
}
```

## Tips & Tricks:
```cs
// If you're viewing this page with IE, this *should* return the hwnd of the browser
IntPtr hWnd = WndSearcher.SearchForWindow("IEFrame", "pinvoke.net: EnumWindows");
```

## Alternative Managed API:
```cs
[DllImport("user32.Dll")]
     [return: MarshalAs(UnmanagedType.Bool)]
     public static extern bool EnumWindows(EnumWindowsProc lpEnumFunc, [MarshalAsAttribute(UnmanagedType.Struct)] ref SearchData data);
```
