
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
static extern IntPtr FindWindow(string lpClassName, string lpWindowName);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
```

## VB Signature:
```cs
End Function
    <DllImport("user32.dll", EntryPoint:="FindWindow", SetLastError:=True, CharSet:=CharSet.Auto)> _
```

## VB Signature:
```cs
End Function
    <DllImport("user32.dll", EntryPoint:="FindWindow", SetLastError:=True, CharSet:=CharSet.Auto)> _
```

## VB Signature:
```cs
End Function
```

## Sample Code (C#):
```cs
public static int FindWindow(string windowName, bool wait)
        {
            int hWnd = FindWindow(null, windowName);
            while (wait && hWnd == 0)
            {
                System.Threading.Thread.Sleep(500);
                hWnd = FindWindow(null, windowName);
            }

            return hWnd;
        }

        // THE FOLLOWING METHOD REFERENCES THE SetForegroundWindow API
        public static bool BringWindowToTop(string windowName, bool wait)
        {
            int hWnd = FindWindow(windowName, wait);
            if (hWnd != 0)
            {
                return SetForegroundWindow((IntPtr)hWnd);
            }
            return false;
        }
```

## Sample Code (C#):
```cs
//Open Up blank Notepad First !
string lpszParentClass = "Notepad";
string lpszParentWindow = "Untitled - Notepad";
string lpszClass = "Edit";

IntPtr ParenthWnd = new IntPtr(0);
IntPtr hWnd = new IntPtr(0);
ParenthWnd = FindWindow(lpszParentClass,lpszParentWindow);
if (ParenthWnd.Equals(IntPtr.Zero))  
     Console.WriteLine("Notepad Not Running");
else
{
     hWnd = FindWindowEx(ParenthWnd,hWnd,lpszClass,"");
     if (hWnd.Equals(IntPtr.Zero))  
     Console.WriteLine("What the F??? Notepad doesn't have an edit component ?");
     else
     {
     Console.WriteLine("Notepad Window: " + ParenthWnd.ToString());
     Console.WriteLine("Edit Control: " + hWnd.ToString());
     }
}

'// VB (chellios at gmail dot com)
'// Open up a blank Notepad!
Dim lpszParentClass As String = "Notepad"
Dim lpszParentWindow As String = "Untitled - Notepad"
Dim lpszClass As String = "Edit"

Dim ParenthWnd As New IntPtr(0)
Dim hWnd As New IntPtr(0)

ParenthWnd = FindWindow(lpszParentClass, lpszParentWindow)

If ParenthWnd.Equals(IntPtr.Zero) Then
    Debug.WriteLine("Notepad Not Running!")
Else
    hWnd = FindWindowEx(ParenthWnd, hWnd, lpszClass, "")

    If hWnd.Equals(IntPtr.Zero)
       Debug.WriteLine("What the F??? Notepad doesn't have an Edit component, how strange.")
    Else
       Debug.WriteLine("Notepad Window: " & ParenthWnd.ToString())
       Debug.WriteLine("Edit Control: " & hWnd.ToString())
    End If
End If
```
