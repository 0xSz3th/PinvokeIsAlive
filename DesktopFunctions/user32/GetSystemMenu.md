
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr GetSystemMenu(IntPtr hWnd, bool bRevert);
```

## VB Signature:
```cs
<DllImport("user32.dll", CallingConvention:=CallingConvention.Cdecl)> _
Private Shared Function GetSystemMenu(ByVal hWnd As IntPtr, ByVal bRevert As Boolean) As IntPtr
End Function
```

## Sample Code:
```cs
public class RemoveXButton
{
    [System.Runtime.InteropServices.DllImport("user32.dll")]
    static extern IntPtr GetSystemMenu(IntPtr hWnd, bool bRevert);
    [System.Runtime.InteropServices.DllImport("user32.dll")]
    static extern int GetMenuItemCount(IntPtr hMenu);
    [System.Runtime.InteropServices.DllImport("user32.dll")]
    static extern bool DrawMenuBar(IntPtr hWnd);
    [System.Runtime.InteropServices.DllImport("user32.dll")]
    static extern bool RemoveMenu(IntPtr hMenu, uint uPosition, uint uFlags);
    private const Int32 MF_BYPOSITION = 0x400;
    private const Int32 MF_REMOVE = 0x1000;

    public static void RemoveCloseButton(Form frm)
    {
        IntPtr hMenu;
        int n;
        hMenu = GetSystemMenu(frm.Handle,false);
        if(hMenu != IntPtr.Zero)
        {
            n = GetMenuItemCount(hMenu);
            if(n > 0)
            {
              RemoveMenu(hMenu, (uint)(n-1), MF_BYPOSITION|MF_REMOVE);
              RemoveMenu(hMenu, (uint)(n-2), MF_BYPOSITION | MF_REMOVE);
              DrawMenuBar(frm.Handle);
            }
        }
    }
}

public class WindowFuncs
{
    [DllImport("user32.dll")]
    static extern IntPtr GetSystemMenu(IntPtr hWnd, bool bRevert);
    [DllImport("user32.dll")]
    static extern bool DrawMenuBar(IntPtr hWnd);
    [DllImport("user32.dll")]
    static extern bool DeleteMenu(IntPtr hMenu, uint uPosition, uint uFlags);
    [DllImport("kernel32.dll")]
    static extern IntPtr GetConsoleWindow();

    private const Int32 MF_GRAYED = 0x1;
    private const Int32 SC_CLOSE = 0xF060;

    public static void RemoveConsoleCloseButton()
    {
        IntPtr handle = GetConsoleWindow();
        IntPtr hMenu = GetSystemMenu(handle, false);

        DeleteMenu(hMenu, SC_CLOSE, MF_GRAYED);
        DrawMenuBar(handle);
    }
}
```
