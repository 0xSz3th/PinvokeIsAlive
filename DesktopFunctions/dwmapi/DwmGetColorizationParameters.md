
## C# Signature:
```cs
[DllImport("dwmapi.dll", EntryPoint = "#127", PreserveSig = false)]
    private static extern void DwmGetColorizationParameters(out DWM_COLORIZATION_PARAMS parameters);
```

## Sample Code:
```cs
[DllImport("dwmapi.dll", EntryPoint = "#127", PreserveSig = false)]
    private static extern void DwmGetColorizationParameters(out DWM_COLORIZATION_PARAMS parameters);

    private struct DWM_COLORIZATION_PARAMS
    {
        public uint clrColor;
        public uint clrAfterGlow;
        public uint nIntensity;
        public uint clrAfterGlowBalance;
        public uint clrBlurBalance;
        public uint clrGlassReflectionIntensity;
        public bool fOpaque;
    }

    public void getParameters()
    {
        DWM_COLORIZATION_PARAMS temp = new DWM_COLORIZATION_PARAMS();
        DwmGetColorizationParameters(out temp);
        StringBuilder sb = new StringBuilder();
        sb.AppendLine(temp.clrColor.ToString());
        sb.AppendLine(temp.clrAfterGlow.ToString());
        sb.AppendLine(temp.nIntensity.ToString());
        sb.AppendLine(temp.clrAfterGlowBalance.ToString());
        sb.AppendLine(temp.clrBlurBalance.ToString());
        sb.AppendLine(temp.clrGlassReflectionIntensity.ToString());
        sb.AppendLine(temp.fOpaque.ToString());
        MessageBox.Show(sb.ToString());
    }
```
