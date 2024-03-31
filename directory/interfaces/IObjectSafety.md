
## C# Definition:
```cs
[ComImport, GuidAttribute("CB5BDC81-93C1-11CF-8F20-00805F2CD064")]
[InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
public interface IObjectSafety
{
  [PreserveSig]
  int GetInterfaceSafetyOptions(ref Guid riid, 
                [MarshalAs(UnmanagedType.U4)] ref int pdwSupportedOptions,
                [MarshalAs(UnmanagedType.U4)] ref int pdwEnabledOptions);

  [PreserveSig()]
  int SetInterfaceSafetyOptions(ref Guid riid,
                [MarshalAs(UnmanagedType.U4)] int dwOptionSetMask,
                [MarshalAs(UnmanagedType.U4)] int dwEnabledOptions);
}
```

## C# Sample Implementation:
```cs
using System;
using System.Runtime.InteropServices;

[ComImport, GuidAttribute("CB5BDC81-93C1-11CF-8F20-00805F2CD064")]
[InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
public interface IObjectSafety
{
  [PreserveSig]
  int GetInterfaceSafetyOptions(ref Guid riid,
                [MarshalAs(UnmanagedType.U4)] ref int pdwSupportedOptions,
                [MarshalAs(UnmanagedType.U4)] ref int pdwEnabledOptions);

  [PreserveSig()]
  int SetInterfaceSafetyOptions(ref Guid riid,
                [MarshalAs(UnmanagedType.U4)] int dwOptionSetMask,
                [MarshalAs(UnmanagedType.U4)] int dwEnabledOptions);
}

public class IObjectSafetyDemo : IObjectSafety
{
  private const string _IID_IDispatch = "{00020400-0000-0000-C000-000000000046}";
  private const string _IID_IDispatchEx = "{a6ef9860-c720-11d0-9337-00a0c90dcaa9}";
  private const string _IID_IPersistStorage = "{0000010A-0000-0000-C000-000000000046}";
  private const string _IID_IPersistStream = "{00000109-0000-0000-C000-000000000046}";
  private const string _IID_IPersistPropertyBag = "{37D84F60-42CB-11CE-8135-00AA004BB851}";

  private const int INTERFACESAFE_FOR_UNTRUSTED_CALLER = 0x00000001;
  private const int INTERFACESAFE_FOR_UNTRUSTED_DATA = 0x00000002;
  private const int S_OK = 0;
  private const int E_FAIL = unchecked((int) 0x80004005);
  private const int E_NOINTERFACE = unchecked((int) 0x80004002); 

  private bool _fSafeForScripting = true;
  private bool _fSafeForInitializing = true;

  public int GetInterfaceSafetyOptions(ref Guid riid,
                       ref int pdwSupportedOptions, 
                       ref int pdwEnabledOptions)
  {
    int Rslt = E_FAIL;

    string strGUID = riid.ToString("B");
    pdwSupportedOptions = INTERFACESAFE_FOR_UNTRUSTED_CALLER | INTERFACESAFE_FOR_UNTRUSTED_DATA;
    switch(strGUID)
      {
    case _IID_IDispatch:
    case _IID_IDispatchEx:
      Rslt = S_OK;
      pdwEnabledOptions = 0;
      if (_fSafeForScripting == true)
        pdwEnabledOptions = INTERFACESAFE_FOR_UNTRUSTED_CALLER;
      break;
      case _IID_IPersistStorage:
      case _IID_IPersistStream:
      case _IID_IPersistPropertyBag:
        Rslt = S_OK;
        pdwEnabledOptions = 0;
        if (_fSafeForInitializing == true)
          pdwEnabledOptions = INTERFACESAFE_FOR_UNTRUSTED_DATA;
        break;
      default:
        Rslt = E_NOINTERFACE;
        break;
      }

    return Rslt;
  }

  public int SetInterfaceSafetyOptions(ref Guid riid,
                       int dwOptionSetMask,
                       int dwEnabledOptions)
  {
    int Rslt = E_FAIL;

    string strGUID = riid.ToString("B");
    switch(strGUID)
    {
      case _IID_IDispatch:
      case _IID_IDispatchEx:
    if (((dwEnabledOptions & dwOptionSetMask) == INTERFACESAFE_FOR_UNTRUSTED_CALLER) &&
         (_fSafeForScripting == true))
      Rslt = S_OK;
    break;
      case _IID_IPersistStorage:
      case _IID_IPersistStream:
      case _IID_IPersistPropertyBag:
    if (((dwEnabledOptions & dwOptionSetMask) == INTERFACESAFE_FOR_UNTRUSTED_DATA) && 
         (_fSafeForInitializing == true))
      Rslt = S_OK;
    break;
      default:
    Rslt = E_NOINTERFACE;
    break;
    }

    return Rslt;
  }

}
```
