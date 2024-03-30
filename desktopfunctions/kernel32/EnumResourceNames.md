
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool EnumResourceNames(IntPtr hModule, string lpszType, EnumResNameProcDelegate lpEnumFunc, IntPtr lParam);

[DllImport("kernel32.dll")]
static extern bool EnumResourceNames(IntPtr hModule, int dwID, EnumResNameProcDelegate lpEnumFunc, IntPtr lParam);
```

## C# User-Defined Types:
```cs
delegate bool EnumResNameProcDelegate(IntPtr hModule, IntPtr lpszType, IntPtr lpszName, IntPtr lParam);

enum ResType
{
    CURSOR = 1,
    BITMAP = 2,
    ICON = 3,
    MENU = 4,
    DIALOG = 5,
    STRING = 6,
    FONTDIR = 7,
    FONT = 8,
    ACCELERATOR = 9,
    RCDATA = 10,
    MESSAGETABLE = 11,
    GROUP_CURSOR = 12,
    GROUP_ICON = 14,
    VERSION = 16,
    DLGINCLUDE = 17,
    PLUGPLAY = 19,
    VXD = 20,
    ANICURSOR = 21,
    ANIICON = 22,
    HTML = 23,
    MANIFEST = 24
}
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", CharSet:=CharSet.Unicode, EntryPoint:="EnumResourceNamesW", SetLastError:=True)> _
Private Shared Function EnumResourceNames(ByVal hModule As IntPtr, ByVal lpszType As String, ByVal lpEnumFunc As EnumResNameProcDelegate, ByVal lParam As IntPtr) As Boolean
End Function

<DllImport("kernel32.dll", CharSet:=CharSet.Unicode, EntryPoint:="EnumResourceNamesW", SetLastError:=True)> _
Private Shared Function EnumResourceNames(ByVal hModule As IntPtr, ByVal dwID As Integer, ByVal lpEnumFunc As EnumResNameProcDelegate, ByVal lParam As IntPtr) As Boolean
End Function
```

## VB.NET User-Defined Types:
```cs
Private Delegate Function EnumResNameProcDelegate(ByVal hModule As IntPtr, ByVal lpszType As IntPtr, ByVal lpszName As IntPtr, ByVal lParam As IntPtr) As Boolean

Public Enum ResourceType
    CURSOR = 1
    BITMAP = 2
    ICON = 3
    MENU = 4
    DIALOG = 5
    [STRING] = 6
    FONTDIR = 7
    FONT = 8
    ACCELERATOR = 9
    RCDATA = 10
    MESSAGETABLE = 11
    GROUP_CURSOR = 12
    GROUP_ICON = 14
    VERSION = 16
    DLGINCLUDE = 17
    PLUGPLAY = 19
    VXD = 20
    ANICURSOR = 21
    ANIICON = 22
    HTML = 23
    MANIFEST = 24
End Enum
```

## VB.NET Sample Code:
```cs
Class Test
    Private Delegate Function EnumResNameProcDelegate(ByVal hModule As IntPtr, ByVal lpszType As IntPtr, ByVal lpszName As IntPtr, ByVal lParam As IntPtr) As Boolean

    <DllImport("kernel32.dll", CharSet:=CharSet.Unicode, EntryPoint:="EnumResourceNamesW", SetLastError:=True)> _
    Private Shared Function EnumResourceNames(ByVal hModule As IntPtr, ByVal lpszType As String, ByVal lpEnumFunc As EnumResNameProcDelegate, ByVal lParam As IntPtr) As Boolean
    End Function

    <DllImport("kernel32.dll", CharSet:=CharSet.Unicode, EntryPoint:="EnumResourceNamesW", SetLastError:=True)> _
    Private Shared Function EnumResourceNames(ByVal hModule As IntPtr, ByVal lpszType As Integer, ByVal lpEnumFunc As EnumResNameProcDelegate, ByVal lParam As IntPtr) As Integer
    End Function

    Private Sub ShowResources()
        Dim dll_hInst As IntPtr

        On Error Resume Next

        dll_hInst = LoadLibraryEx(Filename.Text, 0, 1)

        If Not dll_hInst.Equals(IntPtr.Zero) Then
            EnumResourceNames(dll_hInst, "AVI", AddressOf EnumResNameProc, IntPtr.Zero) 
            FreeLibrary(dll_hInst)
        End If    
    End Sub

    Private Function EnumResNameProc(ByVal hModule As IntPtr, ByVal lpszType As IntPtr, ByVal lpszName As IntPtr, ByVal a As IntPtr) As Boolean
        Dim s As String

        On Error Resume Next

        If (lpszName.ToInt32 > Short.MaxValue) Then
            s = Marshal.PtrToStringUni(lpszName)
        Else
            s = lpszName.ToString()
        End If

        debug.WriteLine(s)

        EnumResNameProc = True
    End Function
End Class
```

## Sample Code:
```cs
using System;
  using System.Runtime.InteropServices;

  namespace EnumResNames_CS
  {
   class Class1
   {
    private const uint RT_CURSOR = 0x00000001;
    private const uint RT_BITMAP = 0x00000002;
    private const uint RT_ICON = 0x00000003;
    private const uint RT_MENU = 0x00000004;
    private const uint RT_DIALOG = 0x00000005;
    private const uint RT_STRING = 0x00000006;
    private const uint RT_FONTDIR = 0x00000007;
    private const uint RT_FONT = 0x00000008;
    private const uint RT_ACCELERATOR = 0x00000009;
    private const uint RT_RCDATA = 0x0000000a;
    private const uint RT_MESSAGETABLE = 0x0000000b;

    private const uint LOAD_LIBRARY_AS_DATAFILE = 0x00000002; 

    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern IntPtr LoadLibraryEx(string lpFileName, IntPtr hFile, uint dwFlags);

    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern bool FreeLibrary(IntPtr hModule);

    [DllImport("kernel32.dll", EntryPoint = "EnumResourceNamesW", CharSet = CharSet.Unicode, SetLastError = true)]
    static extern bool EnumResourceNamesWithName(
      IntPtr hModule, 
      string lpszType,
      EnumResNameDelegate lpEnumFunc, 
      IntPtr lParam);

    [DllImport("kernel32.dll", EntryPoint = "EnumResourceNamesW", CharSet = CharSet.Unicode, SetLastError = true)]
    static extern bool EnumResourceNamesWithID(
      IntPtr hModule, 
      uint lpszType,
      EnumResNameDelegate lpEnumFunc, 
      IntPtr lParam);

    private delegate bool EnumResNameDelegate(
      IntPtr hModule, 
      IntPtr lpszType, 
      IntPtr lpszName,
      IntPtr lParam);

    private static bool IS_INTRESOURCE(IntPtr value)
    {
      if ( ((uint) value) > ushort.MaxValue)
    return false;
      return true;
    }
    private static uint GET_RESOURCE_ID(IntPtr value)
    {
      if (IS_INTRESOURCE(value) == true)
    return (uint) value;
      throw new System.NotSupportedException("value is not an ID!");
    }
    private static string GET_RESOURCE_NAME(IntPtr value)
    {
      if (IS_INTRESOURCE(value) == true)
    return value.ToString();
      return Marshal.PtrToStringUni((IntPtr) value);
    }

    [STAThread]
    static void Main(string[] args)
    {
      IntPtr hMod = LoadLibraryEx(@"D:\Test\StringResource\Debug\StringResource.exe", IntPtr.Zero, LOAD_LIBRARY_AS_DATAFILE);
      if (EnumResourceNamesWithID(hMod, RT_ICON, new EnumResNameDelegate(EnumRes), IntPtr.Zero) == false)
      {
    Console.WriteLine("gle: {0}", Marshal.GetLastWin32Error());
      }
      FreeLibrary(hMod);
    }

    static bool EnumRes(IntPtr hModule, 
      IntPtr lpszType, 
      IntPtr lpszName, 
      IntPtr lParam)
    {
      Console.WriteLine("Type: {0}", GET_RESOURCE_NAME(lpszType));
      Console.WriteLine("Name: {0}", GET_RESOURCE_NAME(lpszName));
      return true;
    }
   }
  }
```
