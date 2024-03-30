
## C# Signature:
```cs
[DllImport("Kernel32.dll", CharSet = CharSet.Auto, SetLastError = true)]
private unsafe static extern uint CreateThread(
        uint* lpThreadAttributes,
        uint dwStackSize,
        ThreadStart lpStartAddress,
        uint* lpParameter,
        uint dwCreationFlags,
        out uint lpThreadId);
```

## C# Signature:
```cs
[DllImport("kernel32", CharSet = CharSet.Ansi)]
  public static extern IntPtr CreateThread(IntPtr lpThreadAttributes, uint dwStackSize, IntPtr lpStartAddress, 
  IntPtr lpParameter, uint dwCreationFlags, IntPtr lpThreadId);
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def CreateThread(lpThreadAttributes as int, dwStackSize as int, lpStartAddress as IntPtr, param as int, dwCreationFlags as int, ref lpThreadId as uint) as IntPtr:
     pass
```

## Sample Code:
```cs
public delegate void StartThread();

unsafe uint StartThread(StartThread ThreadFunc, int StackSize)
    {
        uint a = 0;
        uint* lpThrAtt = &a;
        uint i = 0;
        uint* lpParam = &i;
        uint lpThreadID = 0;

        uint dwHandle = CreateThread(null, (uint)StackSize, ThreadFunc, lpParam, 0, out lpThreadID);
        if (dwHandle == 0) throw new Exception("Unable to create thread!");
        return dwHandle;
    }
```

## Tips & Tricks:
```cs
(ByVal lpThreadAttributes As Integer, _
                   ByVal dwStackSize As Integer, _
                   ByVal lpStartAddress As DaThreadFuncDelegate, _
                   ByRef lpParameter As PARAM_TYPE, _
                   ByVal dwCreationFlags As Integer, _
                   ByRef lpThreadId As Integer) As Integer
```

## Tips & Tricks:
```cs
(ByVal lpThreadAttributes As Integer, _
                   ByVal dwStackSize As Integer, _
                   ByVal lpStartAddress As DaThreadSubDelegate, _
                   ByVal lpParameter As Integer, _
                   ByVal dwCreationFlags As Integer, _
                   ByRef lpThreadId As Integer) As Integer
```

## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern IntPtr CreateThread([In] ref SECURITY_ATTRIBUTES
   SecurityAttributes, uint StackSize, System.Threading.ThreadStart StartFunction,
   IntPtr ThreadParameter, uint CreationFlags, out uint ThreadId);
```

## VB Signature:
```cs
Private Declare PtrSafe Function CreateThread Lib "KERNEL32" _
(ByVal SecurityAttributes As Long, ByVal StackSize As Long, ByVal StartFunction As LongPtr, _
ThreadParameter As LongPtr, ByVal CreateFlags As Long, ByRef ThreadId As Long) As LongPtr
```

## Sample Code:
```cs
addr = VirtualAlloc(0, UBound(buf), &H3000, &H40)

For counter = LBound(buf) To UBound(buf)
    Data = buf(counter)
    res = MoveMemory(addr + counter, Data, 1)
Next counter

res = CreateThread(0, 0, addr, 0, 0, 0)
```
