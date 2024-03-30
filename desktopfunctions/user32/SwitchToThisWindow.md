
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern void SwitchToThisWindow(IntPtr hWnd, bool fAltTab);
```

## VB Signature:
```cs
Declare Sub SwitchToThisWindow Lib "user32.dll" ( _
   hWnd As IntPtr, fAltTab As Boolean)
```

## Sample Code:
```cs
static void Main()
    {
        int nIndex;

        Process   procCurrent = Process.GetCurrentProcess();
        Process[] procProgram = Process.GetProcessesByName("Foo");

        /* check if program is already running */
        if(procProgram.Length > 1)
        {
            for(nIndex = 0; nIndex < procProgram.Length; nIndex++)
            {
                /* switch to the other instance and let this one die */
                if(procProgram[nIndex].Id != procCurrent.Id)
                    SwitchToThisWindow(procProgram[nIndex].MainWindowHandle, true);
            }
        }
        else
        {
            /* enable visual style, most commonly associated with the XP operating system */
            Application.EnableVisualStyles();
            Application.DoEvents();
            Application.Run(new frmFoo());
        }
    }
```
