
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool FreeLibrary(IntPtr hModule);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True, EntryPoint:="FreeLibrary")> _
Public Shared Function FreeLibrary(ByVal hModule As IntPtr) As Boolean
End Function
```

## VB Signature:
```cs
Private Declare Function FreeLibrary Lib "kernel32" (ByVal hLibModule As Long) As Long
```

## Sample Code:
```cs
private void ReadFile() {
      mFiles.Clear();
      hExe = LoadLibrary(mFileName);
      if (hExe.ToInt32() == 0) {
    throw new Win32Exception(Marshal.GetLastWin32Error());
      }
      GCHandle gch = GCHandle.Alloc(mFiles); //convert object to handle
      if (EnumResourceNames(hExe, "FILE", cb, (IntPtr)gch) == false) {
    gch.Free();
    throw new ApplicationException("Error reading files in the installer");
      }
      gch.Free();
      if (FreeLibrary(hExe) == false) {
    throw new Win32Exception(Marshal.GetLastWin32Error());
      }
    }
```
