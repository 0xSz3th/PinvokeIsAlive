
## C# Signature:
```cs
[DllImport("shell32.dll", SetLastError = true)]
static extern IntPtr CommandLineToArgvW(
   [MarshalAs(UnmanagedType.LPWStr)] string lpCmdLine,
   out int pNumArgs);
```

## VB.NET Signature:
```cs
Declare Function CommandLineToArgv Lib "shell32.dll" Alias "CommandLineToArgvW" ( _
    ByVal lpCmdLine As String, _
    ByRef pNumArgs As Integer) As Long
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;
using System.Text;

static class CmdLineToArgvW
{
    // The previous examples on this page used incorrect
    // pointer logic and were removed.

    static string[] SplitArgs(string unsplitArgumentLine)
    {
        int numberOfArgs;
        IntPtr ptrToSplitArgs;
        string[] splitArgs;

        ptrToSplitArgs = CommandLineToArgvW(unsplitArgumentLine, out numberOfArgs);

        // CommandLineToArgvW returns NULL upon failure.
        if (ptrToSplitArgs == IntPtr.Zero)
            throw new ArgumentException("Unable to split argument.", new Win32Exception());

        // Make sure the memory ptrToSplitArgs to is freed, even upon failure.
        try
        {
            splitArgs = new string[numberOfArgs];

            // ptrToSplitArgs is an array of pointers to null terminated Unicode strings.
            // Copy each of these strings into our split argument array.
            for (int i = 0; i < numberOfArgs; i++)
                splitArgs[i] = Marshal.PtrToStringUni(
                    Marshal.ReadIntPtr(ptrToSplitArgs, i * IntPtr.Size));

            return splitArgs;
        }
        finally
        {
            // Free memory obtained by CommandLineToArgW.
            LocalFree(ptrToSplitArgs);
        }
    }

    [DllImport("shell32.dll", SetLastError = true)]
    static extern IntPtr CommandLineToArgvW(
        [MarshalAs(UnmanagedType.LPWStr)] string lpCmdLine,
        out int pNumArgs);

    [DllImport("kernel32.dll")]
    static extern IntPtr LocalFree(IntPtr hMem);
}
```
