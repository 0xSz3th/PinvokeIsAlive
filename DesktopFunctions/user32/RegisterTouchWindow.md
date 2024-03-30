
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern bool RegisterTouchWindow(IntPtr hWnd, RegisterTouchFlags flags);
```

## VB Signature:
```cs
Declare Function RegisterTouchWindow Lib "user32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
TWF_NONE = 0x00000000,

  TWF_FINETOUCH = 0x00000001, //Specifies that hWnd prefers noncoalesced touch input.

  TWF_WANTPALM = 0x00000002 //Setting this flag disables palm rejection which reduces delays for getting WM_TOUCH messages.
```
