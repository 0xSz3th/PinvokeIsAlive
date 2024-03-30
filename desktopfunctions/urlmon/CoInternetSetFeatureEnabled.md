
## C# Signature:
```cs
private const int SET_FEATURE_ON_THREAD = 0x00000001;
private const int SET_FEATURE_ON_PROCESS = 0x00000002;
private const int SET_FEATURE_IN_REGISTRY = 0x00000004;
private const int SET_FEATURE_ON_THREAD_LOCALMACHINE = 0x00000008;
private const int SET_FEATURE_ON_THREAD_INTRANET = 0x00000010;
private const int SET_FEATURE_ON_THREAD_TRUSTED = 0x00000020;
private const int SET_FEATURE_ON_THREAD_INTERNET = 0x00000040;
private const int SET_FEATURE_ON_THREAD_RESTRICTED = 0x00000080;

[DllImport("urlmon.dll")]
[PreserveSig]
[return:MarshalAs(UnmanagedType.Error)]
static extern int CoInternetSetFeatureEnabled(
     INTERNETFEATURELIST FeatureEntry, 
     [MarshalAs(UnmanagedType.U4)] int dwFlags,
     bool fEnable);
```

## VB Signature:
```cs
Declare Function CoInternetSetFeatureEnabled Lib "urlmon.dll" ( _
    ByVal FeatureEntry As INTERNETFEATURELIST, ByVal dwFlags As Long, _
    ByVal fEnable As Long) As Long
```

## Notes:
```cs
The SET_FEATURE_* values are not defined as an enum in urlmon.h, so I kept them as constants.

The return value from CoInternetSetFeatureEnabled should be passed to the static ThrowExceptionForHR method on the Marshal class as well, in case a fail code is returned (or better yet, a wrapper can be created to this method).
```
