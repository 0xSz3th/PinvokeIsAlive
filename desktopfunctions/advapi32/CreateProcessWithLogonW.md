
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true, CharSet=CharSet.Unicode)]
  public static extern bool CreateProcessWithLogonW(
     String             userName,
     String             domain,
     String             password,
     LogonFlags         logonFlags,
     String             applicationName,
     String             commandLine,
     CreationFlags          creationFlags,
     UInt32             environment,
     String             currentDirectory,
     ref  StartupInfo       startupInfo,
     out ProcessInformation     processInformation);
```

## VB Signature:
```cs
<DllImport("advapi32.dll", SetLastError:=True, CharSet:=CharSet.Unicode)> _
    Public Function CreateProcessWithLogonW(ByVal userName As String, ByVal domain As String, ByVal password As String, ByVal logonFlags As UInt32, ByVal applicationName As String, ByVal commandLine As String, ByVal creationFlags As UInt32, ByVal environment As UInt32, ByVal currentDirectory As String, ByRef startupInfo As StartupInfo, ByRef processInformation As ProcessInformation) As Boolean
    End Function
```

## Sample code for VB
```cs
Imports System
Imports System.Runtime.InteropServices

'2005.09.21
'translation in VB of the C# code of
  'Chris Hand cj_hand@hotmail.com

Module Module1

    Public Infinite As System.UInt32 = Convert.ToUInt32(&HFFFFFFF)
    Public Startf_UseStdHandles As Int32 = &H100
    Public StdOutputHandle As Int32 = -11
    Public StdErrorHandle As Int32 = -12

    <StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
    Public Structure StartupInfo
    Public cb As Integer
    Public reserved As String
    Public desktop As String
    Public title As String
    Public x As Integer
    Public y As Integer
    Public xSize As Integer
    Public ySize As Integer
    Public xCountChars As Integer
    Public yCountChars As Integer
    Public fillAttribute As Integer
    Public flags As Integer
    Public showWindow As UInt16
    Public reserved2 As UInt16
    Public reserved3 As Byte
    Public stdInput As IntPtr
    Public stdOutput As IntPtr
    Public stdError As IntPtr
    End Structure 'StartupInfo

    Friend Structure ProcessInformation
    Public process As IntPtr
    Public thread As IntPtr
    Public processId As Integer
    Public threadId As Integer
    End Structure 'ProcessInformation


    <DllImport("advapi32.dll", SetLastError:=True, CharSet:=CharSet.Unicode)> _
    Public Function CreateProcessWithLogonW(ByVal userName As String, ByVal domain As String, ByVal password As String, ByVal logonFlags As UInt32, ByVal applicationName As String, ByVal commandLine As String, ByVal creationFlags As UInt32, ByVal environment As UInt32, ByVal currentDirectory As String, ByRef startupInfo As StartupInfo, ByRef processInformation As ProcessInformation) As Boolean
    End Function


    <DllImport("kernel32.dll", SetLastError:=True)> _
    Public Function GetExitCodeProcess(ByVal process As IntPtr, ByRef exitCode As UInt32) As Boolean
    End Function


    <DllImport("Kernel32.dll", SetLastError:=True)> _
    Public Function WaitForSingleObject(ByVal handle As IntPtr, ByVal milliseconds As UInt32) As UInt32
    End Function


    <DllImport("Kernel32.dll", SetLastError:=True)> _
    Public Function GetStdHandle(ByVal handle As IntPtr) As IntPtr
    End Function


    <DllImport("Kernel32.dll", SetLastError:=True)> _
    Public Function CloseHandle(ByVal handle As IntPtr) As Boolean
    End Function


    <STAThread()> _
    Overloads Sub Main(ByVal args() As String)
    Dim MyPointer As IntPtr = Marshal.AllocHGlobal(4)
    Marshal.WriteInt32(MyPointer, StdOutputHandle)
    Dim MyErrorPointer As IntPtr = Marshal.AllocHGlobal(4)
    Marshal.WriteInt32(MyErrorPointer, StdErrorHandle)
    Dim startupInfo As New StartupInfo
    startupInfo.reserved = Nothing
    startupInfo.flags = startupInfo.flags And Startf_UseStdHandles
    startupInfo.stdOutput = MyPointer  
    startupInfo.stdError = MyErrorPointer     

    Dim exitCode As System.UInt32 = Convert.ToUInt32(123456)
    Dim processInfo As New ProcessInformation

    Dim command As String = "c:\windows\Notepad.exe"
    Dim user As String = "administrator"
    Dim domain As String = System.Environment.MachineName
    Dim password As String = "blank"
    Dim currentDirectory As String = System.IO.Directory.GetCurrentDirectory()

    Try
        CreateProcessWithLogonW(user, domain, password, Convert.ToUInt32(1), _
        command, command, Convert.ToUInt32(0), Convert.ToUInt32(0), _
        currentDirectory, startupInfo, processInfo)
    Catch e As Exception
        Console.WriteLine(e.ToString())
    End Try
    Console.WriteLine("Running ...")
    WaitForSingleObject(processInfo.process, Infinite)
    GetExitCodeProcess(processInfo.process, exitCode)

    Console.WriteLine("Exit code: {0}", exitCode)

    CloseHandle(processInfo.process)
    CloseHandle(processInfo.thread)
    End Sub
```

## User-Defined Types:
```cs
[Flags]
     enum CreationFlags 
    {
        CREATE_SUSPENDED       = 0x00000004,
        CREATE_NEW_CONSOLE     = 0x00000010,
        CREATE_NEW_PROCESS_GROUP   = 0x00000200,
        CREATE_UNICODE_ENVIRONMENT = 0x00000400,
        CREATE_SEPARATE_WOW_VDM    = 0x00000800,
        CREATE_DEFAULT_ERROR_MODE  = 0x04000000,
    }

    [Flags]
    enum LogonFlags 
    {
        LOGON_WITH_PROFILE     = 0x00000001,
        LOGON_NETCREDENTIALS_ONLY  = 0x00000002    
    }
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;

//Chris Hand cj_hand@hotmail.com
//2005.03.13
namespace RunAs
{
    class Class1
    {
        public const UInt32 Infinite = 0xffffffff;
        public const Int32      Startf_UseStdHandles = 0x00000100;
        public const Int32      StdOutputHandle = -11;
        public const Int32      StdErrorHandle = -12;

        [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
        public struct StartupInfo
        {
            public int    cb;
            public String reserved;
            public String desktop;
            public String title;
            public int    x;
            public int    y;
            public int    xSize;
            public int    ySize;
            public int    xCountChars;
            public int    yCountChars;
            public int    fillAttribute;
            public int    flags;
            public UInt16 showWindow;
            public UInt16 reserved2;
            public byte   reserved3;
            public IntPtr stdInput;
            public IntPtr stdOutput;
            public IntPtr stdError;
        } 

        internal struct ProcessInformation
        {
            public IntPtr process;
            public IntPtr thread;
            public int    processId;
            public int    threadId;
        }


        [DllImport("advapi32.dll", SetLastError=true, CharSet=CharSet.Unicode)]
        public static extern bool CreateProcessWithLogonW(
            String userName,
            String domain,
            String password,
            UInt32 logonFlags,
            String applicationName,
            String commandLine,
            UInt32 creationFlags,
            UInt32 environment,
            String currentDirectory,
            ref   StartupInfo startupInfo,
            out  ProcessInformation processInformation);

        [DllImport("kernel32.dll", SetLastError=true)]
        public static extern bool GetExitCodeProcess(IntPtr process, ref UInt32 exitCode);

        [DllImport("Kernel32.dll", SetLastError=true)]
        public static extern UInt32 WaitForSingleObject(IntPtr handle, UInt32 milliseconds);

        [DllImport("Kernel32.dll", SetLastError=true)]
        public static extern IntPtr GetStdHandle(IntPtr handle);

        [DllImport("Kernel32.dll", SetLastError=true)]
        public static extern bool CloseHandle(IntPtr handle);

        [STAThread]
        static void Main(string[] args)
        {
            StartupInfo startupInfo = new StartupInfo();
            startupInfo.reserved = null;
            startupInfo.flags &= Startf_UseStdHandles;
            startupInfo.stdOutput = (IntPtr)StdOutputHandle;
            startupInfo.stdError = (IntPtr)StdErrorHandle;

            UInt32 exitCode = 123456;
            ProcessInformation processInfo = new ProcessInformation();

            String command = @"c:\windows\notepad.exe";
            String user    = "administrator";
            String domain  = System.Environment.MachineName;
            String password = "Blank";
            String currentDirectory = System.IO.Directory.GetCurrentDirectory();

            try
            {
                CreateProcessWithLogonW(
                    user,
                    domain,
                    password,
                    (UInt32) 1,
                    command,
                    command,
                    (UInt32) 0,
                    (UInt32) 0,
                    currentDirectory,
                    ref startupInfo,
                    out processInfo);
            } 
            catch (Exception e)
            {
                Console.WriteLine(e.ToString());
            }

            Console.WriteLine("Running ...");
            WaitForSingleObject(processInfo.process, Infinite);
            GetExitCodeProcess(processInfo.process, ref exitCode);

            Console.WriteLine("Exit code: {0}", exitCode);

            CloseHandle(processInfo.process);
            CloseHandle(processInfo.thread);
        }
    }
}
```
