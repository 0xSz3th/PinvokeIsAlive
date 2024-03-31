
## C# Constants:
```cs
private const int WM_USER = 0x400;
private const int RB_INSERTBANDA = (WM_USER + 1);
private const int RB_DELETEBAND = (WM_USER + 2);
private const int RB_GETBARINFO = (WM_USER + 3);
private const int RB_SETBARINFO = (WM_USER + 4);
private const int RB_SETBANDINFOA = (WM_USER + 6);
private const int RB_SETPARENT = (WM_USER + 7);
private const int RB_HITTEST = (WM_USER + 8);
private const int RB_GETRECT = (WM_USER + 9);
private const int RB_INSERTBANDW = (WM_USER + 10);
private const int RB_SETBANDINFOW = (WM_USER + 11);
private const int RB_GETBANDCOUNT = (WM_USER + 12);
private const int RB_GETROWCOUNT = (WM_USER + 13);
private const int RB_GETROWHEIGHT = (WM_USER + 14);
private const int RB_IDTOINDEX = (WM_USER + 16);
private const int RB_GETTOOLTIPS = (WM_USER + 17);
private const int RB_SETTOOLTIPS = (WM_USER + 18);
private const int RB_SETBKCOLOR = (WM_USER + 19);
private const int RB_GETBKCOLOR = (WM_USER + 20);
private const int RB_SETTEXTCOLOR = (WM_USER + 21);
private const int RB_GETTEXTCOLOR = (WM_USER + 22);
private const int RB_SIZETORECT = (WM_USER + 23);
private const int RB_BEGINDRAG = (WM_USER + 24);
private const int RB_ENDDRAG = (WM_USER + 25);
private const int RB_DRAGMOVE = (WM_USER + 26);
private const int RB_GETBARHEIGHT = (WM_USER + 27);
private const int RB_GETBANDINFOW = (WM_USER + 28);
private const int RB_GETBANDINFOA = (WM_USER + 29);
private const int RB_MINIMIZEBAND = (WM_USER + 30);
private const int RB_MAXIMIZEBAND = (WM_USER + 31);
private const int RB_GETBANDBORDERS = (WM_USER + 34);
private const int RB_SHOWBAND = (WM_USER + 35);
private const int RB_SETPALETTE = (WM_USER + 37);
private const int RB_GETPALETTE = (WM_USER + 38);
private const int RB_MOVEBAND = (WM_USER + 39);
private const int RB_GETBANDMARGINS = (WM_USER + 40);
private const int RB_SETEXTENDEDSTYLE = (WM_USER + 41);
private const int RB_GETEXTENDEDSTYLE = (WM_USER + 42);
private const int RB_PUSHCHEVRON = (WM_USER + 43);
private const int RB_SETBANDWIDTH = (WM_USER + 44);
private static readonly int RB_INSERTBAND = (Marshal.SystemDefaultCharSize == 1) ? RB_INSERTBANDA : RB_INSERTBANDW;
private static readonly int RB_SETBANDINFO = (Marshal.SystemDefaultCharSize == 1) ? RB_SETBANDINFOA : RB_SETBANDINFOW;
private static readonly int RB_GETBANDINFO = (Marshal.SystemDefaultCharSize == 1) ? RB_GETBANDINFOA : RB_GETBANDINFOW;
```

## VB Constants:
```cs
Private Const WM_USER As Integer = 1024
Private Const RB_INSERTBANDA As Integer = (WM_USER + 1)
Private Const RB_DELETEBAND As Integer = (WM_USER + 2)
Private Const RB_GETBARINFO As Integer = (WM_USER + 3)
Private Const RB_SETBARINFO As Integer = (WM_USER + 4)
Private Const RB_SETBANDINFOA As Integer
Private Const RB_SETPARENT As Integer = (WM_USER + 7)
Private Const RB_HITTEST As Integer = (WM_USER + 8)
Private Const RB_GETRECT As Integer = (WM_USER + 9)
Private Const RB_INSERTBANDW As Integer = (WM_USER + 10)
Private Const RB_SETBANDINFOW As Integer
Private Const RB_GETBANDCOUNT As Integer
Private Const RB_GETROWCOUNT As Integer = (WM_USER + 13)
Private Const RB_GETROWHEIGHT As Integer
Private Const RB_IDTOINDEX As Integer = (WM_USER + 16)
Private Const RB_GETTOOLTIPS As Integer = (WM_USER + 17)
Private Const RB_SETTOOLTIPS As Integer = (WM_USER + 18)
Private Const RB_SETBKCOLOR As Integer = (WM_USER + 19)
Private Const RB_GETBKCOLOR As Integer = (WM_USER + 20)
Private Const RB_SETTEXTCOLOR As Integer
Private Const RB_GETTEXTCOLOR As Integer
Private Const RB_SIZETORECT As Integer = (WM_USER + 23)
Private Const RB_BEGINDRAG As Integer = (WM_USER + 24)
Private Const RB_ENDDRAG As Integer = (WM_USER + 25)
Private Const RB_DRAGMOVE As Integer = (WM_USER + 26)
Private Const RB_GETBARHEIGHT As Integer
Private Const RB_GETBANDINFOW As Integer
Private Const RB_GETBANDINFOA As Integer
Private Const RB_MINIMIZEBAND As Integer
Private Const RB_MAXIMIZEBAND As Integer
Private Const RB_GETBANDBORDERS As Integer
Private Const RB_SHOWBAND As Integer = (WM_USER + 35)
Private Const RB_SETPALETTE As Integer = (WM_USER + 37)
Private Const RB_GETPALETTE As Integer = (WM_USER + 38)
Private Const RB_MOVEBAND As Integer = (WM_USER + 39)
Private Const RB_GETBANDMARGINS As Integer = (WM_USER + 40)
Private Const RB_SETEXTENDEDSTYLE As Integer
Private Const RB_GETEXTENDEDSTYLE As Integer
Private Const RB_PUSHCHEVRON As Integer = (WM_USER + 43)
Private Const RB_SETBANDWIDTH As Integer = (WM_USER + 44)
Private Shared ReadOnly RB_INSERTBAND As Integer = If((Marshal.SystemDefaultCharSize = 1), RB_INSERTBANDA, RB_INSERTBANDW)
Private Shared ReadOnly RB_SETBANDINFO As Integer = If((Marshal.SystemDefaultCharSize = 1), RB_SETBANDINFOA, RB_SETBANDINFOW)
Private Shared ReadOnly RB_GETBANDINFO As Integer = If((Marshal.SystemDefaultCharSize = 1), RB_GETBANDINFOA, RB_GETBANDINFOW)
```
