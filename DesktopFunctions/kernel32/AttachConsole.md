
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
    static extern bool AttachConsole(uint dwProcessId);
```

## VB Signature:
```cs
Declare Function AttachConsole Lib "kernel32.dll" (dwProcessId as UInteger) As Boolean
```

## User-Defined Types:
```cs
const uint ATTACH_PARENT_PROCESS = 0x0ffffffff;  // default value if not specifing a process ID
```

## User-Defined Types:
```cs
const int ERROR_ACCESS_DENIED = 5; // process was already attached to another console
```

## Sample Code to Paste in your "Windows Application (C#)" Program.cs right after the lines that say "static class Program { ":
```cs
/// <remarks>
    /// 
    ///  USAGE: Place inside your program's main static class
    ///  and call AllocateConsole whenever you want.
    /// </remarks>

    /// <summary>
    /// allocates a new console for the calling process.
    /// </summary>
    /// <returns>If the function succeeds, the return value is nonzero.
    /// If the function fails, the return value is zero. 
    /// To get extended error information, call Marshal.GetLastWin32Error.</returns>
    [DllImport("kernel32",SetLastError=true)]
    static extern bool AllocConsole();
    /// <summary>
    /// Detaches the calling process from its console
    /// </summary>
    /// <returns>If the function succeeds, the return value is nonzero.
    /// If the function fails, the return value is zero. 
    /// To get extended error information, call Marshal.GetLastWin32Error.</returns>
    [DllImport("kernel32", SetLastError = true)]
    static extern bool FreeConsole();    
    /// <summary>
    /// Attaches the calling process to the console of the specified process.
    /// </summary>
    /// <param name="dwProcessId">[in] Identifier of the process, usually will be ATTACH_PARENT_PROCESS</param>
    /// <returns>If the function succeeds, the return value is nonzero.
    /// If the function fails, the return value is zero. 
    /// To get extended error information, call Marshal.GetLastWin32Error.</returns>
    [DllImport("kernel32.dll", SetLastError=true)]
    static extern bool AttachConsole(uint dwProcessId);
    /// <summary>Identifies the console of the parent of the current process as the console to be attached.
    /// always pass this with AttachConsole in .NET for stability reasons and mainly because
    /// I have NOT tested interprocess attaching in .NET so dont blame me if it doesnt work! </summary>
    const uint ATTACH_PARENT_PROCESS = 0x0ffffffff;  
    /// <summary>
    /// calling process is already attached to a console
    /// </summary>
    const int ERROR_ACCESS_DENIED = 5;  
    /// <summary>
    /// Allocate a console if application started from within windows GUI. 
    /// Detects the presence of an existing console associated with the application and
    /// attaches itself to it if available.
    /// </summary>
    private static void AllocateConsole()
    {
        //
        // the following should only be used in a non-console application type (C#)
        // (since a console is allocated/attached already when you define a console app.. :) )
        //
        if (!AttachConsole(ATTACH_PARENT_PROCESS) && Marshal.GetLastWin32Error() == ERROR_ACCESS_DENIED)
        {
        // A console was not allocated, so we need to make one.
        if (!AllocConsole())
        {
            MessageBox.Show("A console could not be allocated, sorry!");
            throw new Exception("Console Allocation Failed");
        }
        else
        {
            Console.WriteLine("Is Attached, press a key...");
            Console.ReadKey(true);
            // you now may use the Console.xxx functions from .NET framework
            // and they will work as normal
        }

        }
    }
```

## Author
```cs
[ mailto:Gabriel@paradisim.net ]
     or visit www.paradisim.net or 
        [ http://inversegoogle.paradisim.net/index3.htm ]
      for a snazzy black google search engine *yeah* i _did_ say snazzy, 
      i know i know... sheesh.

The FreeConsole API4/18/2010 9:54:09 PM - -87.74.96.9Attach current process to the console of a specified process, or to the current one by default (see ATTACH_PARENT_PROCESS) (this is an large contrib article, and since the net add-in insists on using this one, i decided to place it here and not in the original place.)5/18/2020 12:05:07 PM - LNK1123-84.26.94.125TODO - a short description12/2/2007 1:13:05 PM - anonymous
```
