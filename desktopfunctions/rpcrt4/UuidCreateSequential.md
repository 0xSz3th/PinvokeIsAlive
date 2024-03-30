
## C# Signature:
```cs
[DllImport("rpcrt4.dll", SetLastError=true)]
static extern int UuidCreateSequential(out Guid guid);
```

## VB Signature:
```cs
Declare Function UuidCreateSequential Lib "rpcrt4.dll" (ByRef id As Guid) As Integer
```

## Notes:
```cs
92E60A8A-2A99-4F53-9A71-AC69BD7E4D75
BB88FD63-DAC2-4B15-8ADF-1D502E64B92F
28F8800C-C804-4F0F-B6F1-24BFC4D4EE80
EBD133A6-6CF3-4ADA-B723-A8177B70D268
B10A35C0-F012-4EC1-9D24-3CC91D2B7122
```

## Notes:
```cs
19F287B4-8830-11D9-8BFC-000CF1ADC5B7
19F287B5-8830-11D9-8BFC-000CF1ADC5B7
19F287B6-8830-11D9-8BFC-000CF1ADC5B7
19F287B7-8830-11D9-8BFC-000CF1ADC5B7
19F287B8-8830-11D9-8BFC-000CF1ADC5B7
```

## Sample Code in C#:
```cs
static Guid UuidCreateSequential()
{
   const int RPC_S_OK = 0;
   Guid g;
   int hr = UuidCreateSequential(out g);
   if (hr != RPC_S_OK)
     throw new ApplicationException
       ("UuidCreateSequential failed: " + hr);
   return g;
}
```

## Sample Code in VB:
```cs
Sub Main()
   Dim myId As Guid
   Dim code As Integer
   code = UuidCreateSequential(myId)
   If code <> 0 Then
     Console.WriteLine("UuidCreateSequential failed: {0}", code)
   Else
     Console.WriteLine(myId)
   End If
End Sub
```
