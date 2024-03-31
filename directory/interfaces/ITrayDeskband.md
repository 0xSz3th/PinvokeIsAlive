
## C# Definition:
```cs
[ComImport, Guid("6D67E846-5B9C-4db8-9CBC-DDE12F4254F1"),
     InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface ITrayDeskband
    {
      [PreserveSig]
      int ShowDeskBand([In, MarshalAs(UnmanagedType.Struct)] ref Guid clsid);
      [PreserveSig]
      int HideDeskBand([In, MarshalAs(UnmanagedType.Struct)] ref Guid clsid);
      [PreserveSig]
      int IsDeskBandShown([In, MarshalAs(UnmanagedType.Struct)] ref Guid clsid);
      [PreserveSig]
      int DeskBandRegistrationChanged();
    }
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface ITrayDeskband
   TODO
End Interface
```

## Sample-Code:
```cs
ITrayDeskband obj = null;
    Type trayDeskbandType = System.Type.GetTypeFromCLSID(new Guid("E6442437-6C68-4f52-94DD-2CFED267EFB9"));
    try
    {
        obj = (ITrayDeskband)Activator.CreateInstance(trayDeskbandType);
        Guid deskbandGuid = {SomeDeskbandGuid}
        obj.DeskBandRegistrationChanged();
        hr = obj.ShowDeskBand(ref deskbandGuid);
        if (hr != 0)
            throw new Exception("Error while trying to show deskband: " + hr);
        obj.DeskBandRegistrationChanged();
    }
    catch (Exception e)
    {
        MessageBox.Show(e.Message);
    }
    finally
    {
        if (obj != null && Marshal.IsComObject(obj))
            Marshal.ReleaseComObject(obj);
    }
```
