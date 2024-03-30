
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
internal static extern Int32 GetApplicationUserModelId(
    IntPtr hProcess, 
    ref UInt32 AppModelIDLength, 
    [MarshalAs(UnmanagedType.LPWStr)] StringBuilder sbAppUserModelID);
```

## VB Signature:
```cs
Declare Function GetApplicationUserModelId Lib "kernel32.dll" (TODO) As TODO
```

## Sample Code:
```cs
const int QueryLimitedInformation = 0x1000;
   const int ERROR_INSUFFICIENT_BUFFER = 0x7a;
   const int ERROR_SUCCESS = 0x0;

   [DllImport("kernel32.dll")]
   internal static extern IntPtr OpenProcess(int dwDesiredAccess, bool bInheritHandle, int dwProcessId);

   [DllImport("kernel32.dll")]
   static extern bool CloseHandle(IntPtr hHandle);

   if (sProcessName.ToLower().Contains("wwahost") 
        && ((Environment.OSVersion.Version.Major == 6) && (Environment.OSVersion.Version.Minor > 1)))
        {
        IntPtr ptrProcess = OpenProcess(QueryLimitedInformation, false, iPID);
        if (IntPtr.Zero != ptrProcess)
        {
            uint cchLen = 130;
            StringBuilder sbName = new StringBuilder((int)cchLen);
            Int32 lResult = GetApplicationUserModelId(ptrProcess, ref cchLen, sbName);
            if (ERROR_SUCCESS == lResult)
            {
            sResult = sbName.ToString();
            }
            else if (ERROR_INSUFFICIENT_BUFFER == lResult)
            {
            sbName = new StringBuilder((int)cchLen);
            if (ERROR_SUCCESS == GetApplicationUserModelId(ptrProcess, ref cchLen, sbName))
            {
                sResult = sbName.ToString();
            }
            }
            CloseHandle(ptrProcess);
        }
        }
```
