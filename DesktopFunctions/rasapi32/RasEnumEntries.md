
## C# Signature:
```cs
[DllImport("rasapi32.dll", SetLastError=true,CharSet=CharSet.Auto)]
static extern uint RasEnumEntries(
    IntPtr reserved,
    IntPtr lpszPhonebook,
    [In,Out] RASENTRYNAME[] lprasentryname,
    ref int lpcb,
    ref int lpcEntries);
```

## VB Signature:
```cs
<DllImport("rasapi32.dll", EntryPoint:="RasEnumEntries", CharSet:=CharSet.Auto)> _
Private Shared Function RasEnumEntries( _
     ByVal reserved As String, _
     ByVal lpszPhoneBook As String, _
     ByVal lpRasEntryName As IntPtr, _
     ByRef lpc As Int32, _
     ByRef lpcEntries As Int32) As ReturnCodes
End Function
```

## Tips & Tricks:
```cs
const int MAX_PATH = 260;
    const int RAS_MaxEntryName = 256;

    [StructLayout(LayoutKind.Sequential,CharSet=CharSet.Auto)]
    struct RASENTRYNAME { 
        public int     dwSize; 
        [MarshalAs(UnmanagedType.ByValTStr,SizeConst=RAS_MaxEntryName + 1)]
        public string    szEntryName; 
        public int     dwFlags;     
        [MarshalAs(UnmanagedType.ByValTStr,SizeConst=MAX_PATH + 1)]
        public string    szPhonebook;
    }
```

## Sample Code:
```cs
using System;
    using System.Runtime.InteropServices;

    class RasEnumEntriesSample
    {
    const int MAX_PATH = 260;
    const int RAS_MaxEntryName = 256;

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
    struct RASENTRYNAME
    {
        public int dwSize;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = RAS_MaxEntryName + 1)]
        public string szEntryName;
        public int dwFlags;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MAX_PATH + 1)]
        public string szPhonebook;
    }
```

## Sample Code:
```cs
[DllImport("rasapi32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    static extern uint RasEnumEntries(IntPtr reserved, IntPtr lpszPhonebook,
        [In, Out] RASENTRYNAME[] lprasentryname, ref int lpcb, ref int lpcEntries);

    [STAThread]
    static void Main(string[] args)
    {
        int cb = Marshal.SizeOf(typeof(RASENTRYNAME)), entries = 0;
        RASENTRYNAME[] entryNames = new RASENTRYNAME[1];
        entryNames[0].dwSize = Marshal.SizeOf(typeof(RASENTRYNAME));
        //Get entry number
        uint nRet = RasEnumEntries(IntPtr.Zero, IntPtr.Zero, entryNames, ref cb, ref entries);
        if (entries == 0) return;
        string[] _EntryNames = new string[entries];
        entryNames = new RASENTRYNAME[entries];
        for (int i = 0; i < entries; i++)
        {
        entryNames[i].dwSize = Marshal.SizeOf(typeof(RASENTRYNAME));
        }

        nRet = RasEnumEntries(IntPtr.Zero, IntPtr.Zero, entryNames, ref cb, ref entries);
        for (int i = 0; i < entries; i++)
        {
        _EntryNames[i] = entryNames[i].szEntryName;
        Console.WriteLine(_EntryNames[i]);
        }
        Console.ReadKey();
    }

    }
```
