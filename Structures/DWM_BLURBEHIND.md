
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    struct DWM_BLURBEHIND
    {
        public DWM_BB dwFlags;
        public bool fEnable;
        public IntPtr hRgnBlur;
        public bool fTransitionOnMaximized;

        public DWM_BLURBEHIND(bool enabled)
        {
        fEnable = enabled ? true : false;
        hRgnBlur = IntPtr.Zero;
        fTransitionOnMaximized = false;
        dwFlags = DWM_BB.Enable;
        }

        public System.Drawing.Region Region
        {
        get { return System.Drawing.Region.FromHrgn(hRgnBlur); }
        }

        public bool TransitionOnMaximized
        {
        get { return fTransitionOnMaximized; }
        set
        {
            fTransitionOnMaximized = value ? true : false;
            dwFlags |= DWM_BB.TransitionMaximized;
        }
        }

        public void SetRegion(System.Drawing.Graphics graphics, System.Drawing.Region region)
        {
        hRgnBlur = region.GetHrgn(graphics);
        dwFlags |= DWM_BB.BlurRegion;
        }
    }
```

## VB.NET Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Structure DWM_BLURBEHIND
    Public dwFlags As DWM_BB
    Public fEnable As Boolean
    Public hRgnBlur As IntPtr
    Public fTransitionOnMaximized As Boolean
End Structure
```
