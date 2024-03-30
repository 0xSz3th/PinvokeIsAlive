
## C# Signature:
```cs
[DllImport("dwmapi.dll", EntryPoint = "#131", PreserveSig = false)]
    private static extern void DwmSetColorizationParameters(ref DWM_COLORIZATION_PARAMS parameters,bool unknown);
```

## Sample Code:
```cs
[DllImport("dwmapi.dll", EntryPoint = "#131", PreserveSig = false)]
    private static extern void DwmSetColorizationParameters(ref DWM_COLORIZATION_PARAMS parameters,bool unknown);

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

    public void SetParameters(object sender, EventArgs e)
    {
        DWM_COLORIZATION_PARAMS temp = new DWM_COLORIZATION_PARAMS();
        temp.clrColor = 1802811644;
        temp.clrAfterGlow = 1802811644;
        temp.nIntensity = 8;
        temp.clrAfterGlowBalance = 43;
        temp.clrBlurBalance = 49;
        temp.clrGlassReflectionIntensity = 50;
        temp.fOpaque = false;

        DwmSetColorizationParameters(ref temp, false);

    }
```
