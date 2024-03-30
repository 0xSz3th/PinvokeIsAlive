
## C# Signature:
```cs
[DllImport("kernel32.dll")]
// static extern uint GetLogicalDriveStrings(uint nBufferLength, 
//    [Out] StringBuilder lpBuffer); --- Don't do this!

// if we were to use the StringBuilder, only the first string would be returned
// so, since arrays are reference types, we can pass an array of chars
// just initialize it prior to call the function as
// char[] lpBuffer = new char[nBufferLength];
static extern uint GetLogicalDriveStrings(uint nBufferLength, [Out] char[] lpBuffer);
```

## Sample Code:
```cs
using System;
using System.Collections.Specialized;
using System.Runtime.InteropServices;

public class Mainline
{
[DllImport("kernel32.dll")]
static extern uint GetLogicalDriveStrings(uint nBufferLength, [Out] char[] lpBuffer);

public static void Main()
{
    const int size = 512;
    char[] buffer = new char[size];
    uint code = GetLogicalDriveStrings(size, buffer);

    if (code == 0)
    {
       Console.WriteLine("Call failed");
       return;
    }

    StringCollection list = new StringCollection();
    int start = 0;
    for (int i = 0;  i < code;  ++i)
    {
       if (buffer[i] == 0)
       {
          string s = new string(buffer, start, i - start);
          list.Add(s);
          start = i + 1;
       }
    }

    foreach (string s in list)
       Console.WriteLine(s);
}
}
```
