# IQueryInfo

\[ComImport(),     Guid("00021500-0000-0000-C000-000000000046"),     InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]     interface IQueryInfo     {         \[PreserveSig]         int GetInfoTip(             int dwFlags,             \[MarshalAs( UnmanagedType.LPWStr )] out string ppwszTip );

&#x20;       \[PreserveSig]         int GetInfoFlags( out int pdwFlags );     }

&#x20;   // ppwszTip will be freed by marshler using CoTaskMemFree()
