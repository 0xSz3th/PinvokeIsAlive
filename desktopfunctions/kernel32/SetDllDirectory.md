
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool SetDllDirectory(string lpPathName);
```

## VB Signature:
```cs
Declare Function SetDllDirectory Lib "kernel32.dll" (TODO) As TODO
```

## Sample Code:
```cs
bool did_it_work;
     //set the dll path so it can find the dlls
     did_it_work = SetDllDirectory(@"C:\SomeWhere\");
```
