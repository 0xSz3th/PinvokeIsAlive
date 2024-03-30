
## C# Signature:
```cs
[DllImport("ntdll.dll", SetLastError=true)]
public static extern uint NtQuerySystemTime(out long SystemTime);
```

## VB Signature:
```cs
Declare Function NtQuerySystemTime Lib "ntdll.dll" (Currency) As TODO
```

## Sample Code:
```cs
long t;
NtQuerySystemTime(out t);
MessageBox.Show(DateTime.FromFileTime(t).ToString());
```
