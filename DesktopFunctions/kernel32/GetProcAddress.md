
## C# Signature:
```cs
[DllImport("kernel32", CharSet=CharSet.Ansi, ExactSpelling=true, SetLastError=true)]
static extern IntPtr GetProcAddress(IntPtr hModule, string procName);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True, CharSet:=CharSet.Ansi, ExactSpelling:=True)> _
Private Function GetProcAddress(ByVal hModule As IntPtr, ByVal procName As String) As UIntPtr
End Function
```

## VB Signature:
```cs
Private Declare Function GetProcAddress Lib "kernel32" (ByVal hModule As Integer, ByVal lpProcName As String) As Integer
```

## C++ Signature:
```cs
[DllImport("KERNEL32.DLL", CharSet=CharSet::Ansi, EntryPoint="GetProcAddress", ExactSpelling=true)]
static IntPtr GetProcAddress(IntPtr hModule, String^ lpProcName);
```

## Boo Signature:
```cs
[DllImport("kernel32.dll", CharSet : CharSet.Ansi, ExactSpelling : true)]
static def GetProcAddress(hModule as IntPtr, procName as string) as IntPtr:
     pass
```

## Tips & Tricks:
```cs
internal static class UnsafeNativeMethods {
   [DllImport("kernel32", CharSet=CharSet.Ansi, ExactSpelling=true, SetLastError=true)]
   internal static extern IntPtr GetProcAddress(IntPtr hModule, string procName );
}

internal delegate int DllRegisterServerInvoker();

// code snippet in a method somewhere, error checking omitted
IntPtr fptr = UnsafeNativeMethods.GetProcAddress( hModule, "DllRegisterServer" );
DllRegisterServerInvoker drs = (DllRegisterServerInvoker) Marshal.GetDelegateForFunctionPointer( fptr, typeof(DllRegisterServerInvoker) );
drs(); // call via a function pointer
```

## Tips & Tricks:
```cs
[DllImport("kernel32", SetLastError = true, EntryPoint = "GetProcAddress")]
static extern IntPtr GetProcAddressOrdinal(IntPtr hModule, IntPtr procName);
```

## Sample Code:
```cs
static HMODULE hDLL;
typedef HRESULT (STDAPICALLTYPE * LPFNTEST) (void);
LPFNTEST _pfnTest;

hDLL = LoadLibrary("MyDLL.dll");
_pfnTest = (LPFNTEST)::GetProcAddress(hDLL, "Test");
```
