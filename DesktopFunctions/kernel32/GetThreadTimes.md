
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
static extern bool GetThreadTimes(IntPtr hThread, out long lpCreationTime,
   out long lpExitTime, out long lpKernelTime, out long lpUserTime);
```

## Sample Code:
```cs
long l,KernelStart,UserStart;
GetThreadTimes(GetCurrentThread(),out l,out l,out KernelStart,out UserStart);
try
{
    FunctionToProfile(); // Whatever function you want to measure CPU usage of.
}
finally
{
    long KernelEnd,UserEnd;
    GetThreadTimes(GetCurrentThread(),out l,out l,out KernelEnd,out UserEnd);
    long TimeUsed=(KernelEnd-KernelStart)+(UserEnd-UserStart);
    Console.WriteLine("Function used {0}ms CPU",TimeUsed/10000.0);
}
```
