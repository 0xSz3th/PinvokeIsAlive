
## C# Signature:
```cs
[DllImport("setupapi.dll", SetLastError=true)]
static extern bool SetupDiCallClassInstaller(
     UInt32 InstallFunction,
     IntPtr DeviceInfoSet,
     ref SP_DEVINFO_DATA DeviceInfoData
);
```

## VB Signature:
```cs
<DllImport("setupapi.dll")> _
Public Shared Function SetupDiCallClassInstaller(ByVal InstallFunction As Integer, _ 
                          ByVal DeviceInfoSet As Integer, _ 
                          ByRef DeviceInfoData As SP_DEVINFO_DATA _
                         ) As Boolean
End Function

Or...

<DllImport("setupapi.dll")> _
Public Shared Function SetupDiCallClassInstaller(ByVal InstallFunction As IntPtr, _ 
                          ByVal DeviceInfoSet As IntPtr, _ 
                          ByRef DeviceInfoData As SP_DEVINFO_DATA _
                         ) As Boolean
End Function
```

## Sample Code:
```cs
//
    // http://www.codeproject.com/KB/cs/HardwareHelper.aspx
    //
    //Name:     ChangeIt
    //Inputs:   pointer to hdev, SP_DEV_INFO, bool
    //Outputs:  bool
    //Errors:   This method may throw the following exceptions.
    //      Unable to change device state!
    //Remarks:  Attempts to enable or disable a device driver.  
    //      IMPORTANT NOTE!!!   This code currently does not check the reboot flag.
    //      =================   Some devices require you reboot the OS for the change
    //                  to take affect.  If this describes your device, you 
    //                  will need to look at the SDK call:
    //                  SetupDiGetDeviceInstallParams.  You can call it 
    //                  directly after ChangeIt to see whether or not you need 
    //                  to reboot the OS for you change to go into effect.
    private bool ChangeIt(IntPtr hDevInfo, Native.SP_DEVINFO_DATA devInfoData, bool bEnable)
    {
        try
        {
        //Marshalling vars
        int szOfPcp;
        IntPtr ptrToPcp;
        int szDevInfoData;
        IntPtr ptrToDevInfoData;

        Native.SP_PROPCHANGE_PARAMS pcp = new Native.SP_PROPCHANGE_PARAMS();
        if (bEnable)
        {
            pcp.ClassInstallHeader.cbSize = Marshal.SizeOf(typeof(Native.SP_CLASSINSTALL_HEADER));
            pcp.ClassInstallHeader.InstallFunction = Native.DIF_PROPERTYCHANGE;
            pcp.StateChange = Native.DICS_ENABLE;
            pcp.Scope = Native.DICS_FLAG_GLOBAL;
            pcp.HwProfile = 0;

            //Marshal the params
            szOfPcp = Marshal.SizeOf(pcp);
            ptrToPcp = Marshal.AllocHGlobal(szOfPcp);
            Marshal.StructureToPtr(pcp, ptrToPcp, true);
            szDevInfoData = Marshal.SizeOf(devInfoData);
            ptrToDevInfoData = Marshal.AllocHGlobal(szDevInfoData);

            if (Native.SetupDiSetClassInstallParams(hDevInfo, ptrToDevInfoData, ptrToPcp, Marshal.SizeOf(typeof(Native.SP_PROPCHANGE_PARAMS))))
            {
            Native.SetupDiCallClassInstaller(Native.DIF_PROPERTYCHANGE, hDevInfo, ptrToDevInfoData);
            }
            pcp.ClassInstallHeader.cbSize = Marshal.SizeOf(typeof(Native.SP_CLASSINSTALL_HEADER));
            pcp.ClassInstallHeader.InstallFunction = Native.DIF_PROPERTYCHANGE;
            pcp.StateChange = Native.DICS_ENABLE;
            pcp.Scope = Native.DICS_FLAG_CONFIGSPECIFIC;
            pcp.HwProfile = 0;
        }
        else
        {
            pcp.ClassInstallHeader.cbSize = Marshal.SizeOf(typeof(Native.SP_CLASSINSTALL_HEADER));
            pcp.ClassInstallHeader.InstallFunction = Native.DIF_PROPERTYCHANGE;
            pcp.StateChange = Native.DICS_DISABLE;
            pcp.Scope = Native.DICS_FLAG_CONFIGSPECIFIC;
            pcp.HwProfile = 0;
        }
        //Marshal the params
        szOfPcp = Marshal.SizeOf(pcp);
        ptrToPcp = Marshal.AllocHGlobal(szOfPcp);
        Marshal.StructureToPtr(pcp, ptrToPcp, true);
        szDevInfoData = Marshal.SizeOf(devInfoData);
        ptrToDevInfoData = Marshal.AllocHGlobal(szDevInfoData);
        Marshal.StructureToPtr(devInfoData, ptrToDevInfoData,true);

        bool rslt1 = Native.SetupDiSetClassInstallParams(hDevInfo, ptrToDevInfoData, ptrToPcp, Marshal.SizeOf(typeof(Native.SP_PROPCHANGE_PARAMS)));
        bool rstl2 = Native.SetupDiCallClassInstaller(Native.DIF_PROPERTYCHANGE, hDevInfo, ptrToDevInfoData);
        if ((!rslt1) || (!rstl2))
        {
            throw new Exception("Unable to change device state!");
            return false;
        }
        else
        {
            return true;
        }
        }
        catch (Exception ex)
        {
        return false;
        }
    }
```
