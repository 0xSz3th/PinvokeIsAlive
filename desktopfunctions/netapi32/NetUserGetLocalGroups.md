
## C# Signature:
```cs
[DllImport("Netapi32.dll", SetLastError=true)]
        public extern static int NetUserGetLocalGroups([MarshalAs(UnmanagedType.LPWStr)] string servername,
            [MarshalAs(UnmanagedType.LPWStr)] string username, 
            int level, 
            int flags, 
            out IntPtr bufptr, 
            UInt32 prefmaxlen, 
            out int entriesread, 
            out int totalentries);
```

## VB Signature:
```cs
<DllImport("Netapi32.dll", SetLastError := True)> _
        Public Shared Function NetUserGetLocalGroups(
            <MarshalAs(UnmanagedType.LPWStr)> ByVal servername As String,
            <MarshalAs(UnmanagedType.LPWStr)> ByVal username As String, _
            ByVal level As Integer, _
            ByVal flags As Integer, _
            ByRef bufptr As IntPtr, _
            ByVal prefmaxlen As Integer, _
            ByRef entriesread As Integer, _
            ByRef totalentries As Integer) As Integer
        End Function
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
    internal struct LOCALGROUP_USERS_INFO_0
    {
        [MarshalAs(UnmanagedType.LPWStr)]internal string name;
    }

    [StructLayout(LayoutKind.Sequential)]
    internal struct LOCALGROUP_USERS_INFO_1
    {
        [MarshalAs(UnmanagedType.LPWStr)] public string name;
        [MarshalAs(UnmanagedType.LPWStr)] public string comment;
    }
```

## Sample Code:
```cs
//Example code to place in a class.
        #region  pInvoke Items

        [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
        public struct LOCALGROUP_USERS_INFO_0
        {
            public string groupname;
        }

        [DllImport("Netapi32.dll", SetLastError=true)]
        public extern static int NetUserGetLocalGroups
            ([MarshalAs(UnmanagedType.LPWStr)] string servername,
             [MarshalAs(UnmanagedType.LPWStr)] string username,
             int level,
             int flags, 
             out IntPtr bufptr,
             int prefmaxlen,
             out int entriesread,
             out int totalentries);

        [DllImport("Netapi32.dll", SetLastError=true)]
        public static extern int NetApiBufferFree(IntPtr Buffer);

        #endregion

        private ArrayList GetUserLocalGroups(string ServerName,string Username, int Flags)
        {
            ArrayList myList = new ArrayList();
            int EntriesRead;
            int TotalEntries;
            IntPtr bufPtr;

            ErrorCode = NetUserGetLocalGroups(ServerName,Username,0,Flags,out bufPtr,-1,out EntriesRead, out TotalEntries);
            if(ErrorCode==0)
            {
                _ErrorMessage="Successful";
            }
            else
            {
                _ErrorMessage="Username or computer not found";
            }
            if(Flags>1)
                _ErrorMessage="Flags can only be 0 or 1";
            if(EntriesRead> 0)
            {
                LOCALGROUP_USERS_INFO_0[] RetGroups = new LOCALGROUP_USERS_INFO_0[EntriesRead];
                IntPtr iter = bufPtr;
                for(int i=0; i < EntriesRead; i++)
                {
                    var itemPtr = iter + (Marshal.SizeOf(typeof(LOCALGROUP_USERS_INFO_0)) * i)
                    RetGroups[i] = (LOCALGROUP_USERS_INFO_0)Marshal.PtrToStructure(itemPtr, typeof(LOCALGROUP_USERS_INFO_0));
                    myList.Add(RetGroups[i].groupname);
                }
                NetApiBufferFree(bufPtr);
            }
            return myList;
        }

        ////////////////////////////////////////////////////////////////////////////////////////////////////////

        //Example code for calling application
            ArrayList RetGroups = new ArrayList();
            RetGroups =DsDomain.GetUserLocalGroup(null,"administrator",0);
            foreach(string str in RetGroups)
            {
                Console.WriteLine(str);
            }
```

## Sample Powershell Code
```cs
$TypeDefinition=@"
        using System;
        using System.Runtime.InteropServices;
        using System.Collections;
        using System.Net.Sockets;

        //LG_INCLUDE_INDIRECT=1

        namespace Netapi32 {

          [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
            internal struct LOCALGROUP_USERS_INFO_0 {
              [MarshalAs(UnmanagedType.LPWStr)]internal string name;
            }

          [StructLayout(LayoutKind.Sequential)]
            internal struct LOCALGROUP_USERS_INFO_1 {
              [MarshalAs(UnmanagedType.LPWStr)] public string name;
              [MarshalAs(UnmanagedType.LPWStr)] public string comment;
            }

          public static class api {

            [DllImport("Netapi32.dll", SetLastError=true)]
            public extern static int NetUserGetLocalGroups
               ([MarshalAs(UnmanagedType.LPWStr)] string servername,
            [MarshalAs(UnmanagedType.LPWStr)] string username,
            int level,
            int flags,
            out IntPtr bufptr,
            int prefmaxlen,
            out int entriesread,
            out int totalentries);

            [DllImport("Netapi32.dll", SetLastError=true)]
            public static extern int NetApiBufferFree(IntPtr Buffer);
          }

          public class NetUtil : IDisposable {

            // Creates a new wrapper for the local machine
            public NetUtil() { }

            // Disposes of this wrapper
            public void Dispose() { GC.SuppressFinalize(this); }

            public ArrayList GetUserLocalGroups(string ServerName, string Username, int Flags) {

              ArrayList myList = new ArrayList();
              int EntriesRead;
              int TotalEntries;
              IntPtr bufPtr;
              //int ErrorCode;
              //string _ErrorMessage;

              api.NetUserGetLocalGroups(ServerName,Username,0,Flags,out bufPtr,1024,out EntriesRead, out TotalEntries);
              //ErrorCode = api.NetUserGetLocalGroups(ServerName,Username,0,Flags,out bufPtr,1024,out EntriesRead, out TotalEntries);
              //if (ErrorCode==0) { _ErrorMessage="Successful"; }
              //else { _ErrorMessage="Username or computer not found"; }

              //if (Flags>1) _ErrorMessage="Flags can only be 0 or 1";

              if (EntriesRead> 0) {
            LOCALGROUP_USERS_INFO_0[] RetGroups = new LOCALGROUP_USERS_INFO_0[EntriesRead];
            IntPtr iter = bufPtr;
            for(int i=0; i < EntriesRead; i++) {
              RetGroups[i] = (LOCALGROUP_USERS_INFO_0)Marshal.PtrToStructure(iter, typeof(LOCALGROUP_USERS_INFO_0));
              iter = (IntPtr)((int)iter + Marshal.SizeOf(typeof(LOCALGROUP_USERS_INFO_0)));
              myList.Add(RetGroups[i].name);
            }

            api.NetApiBufferFree(bufPtr);
              }

              return myList;
            } //GetUserLocalGroups

            // Occurs on destruction of the Wrapper
              ~NetUtil() { Dispose(); }

          } // wrapper class
        } // namespace
        "@

        Add-Type -TypeDefinition $TypeDefinition -PassThru
        #$Netapi=new-object Netapi32.NetUtil
```

## Sample PowerShell Code for x64 systems
```cs
$TypeDefinition=@"
        using System;
        using System.Runtime.InteropServices;
        using System.Collections;

        //LG_INCLUDE_INDIRECT=1
        namespace Netapi32Wrapper {

            [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
            internal struct LOCALGROUP_USERS_INFO_0 {
            [MarshalAs(UnmanagedType.LPWStr)]
            internal string name;
            }

            public static class api {

            [DllImport("Netapi32.dll", SetLastError = true)]
            public extern static Int64 NetUserGetLocalGroups(
                [MarshalAs(UnmanagedType.LPWStr)] string servername,
                [MarshalAs(UnmanagedType.LPWStr)] string username,
                Int64 level,
                Int64 flags,
                out IntPtr bufptr,
                Int64 prefmaxlen,
                out Int64 entriesread,
                out Int64 totalentries);

            [DllImport("Netapi32.dll", SetLastError = true)]
            public static extern Int64 NetApiBufferFree(IntPtr Buffer);
            }

            public class NetUtilWrapper : IDisposable {

            // Creates a new wrapper for the local machine
            public NetUtilWrapper() { }

            // Disposes of this wrapper
            public void Dispose() { GC.SuppressFinalize(this); }

            public ArrayList GetUserLocalGroups(string ServerName, string Username, Int64 Flags) {

                ArrayList myList = new ArrayList();
                Int64 EntriesRead;
                Int64 TotalEntries;
                IntPtr bufPtr;
                //int ErrorCode;
                //string _ErrorMessage;

                api.NetUserGetLocalGroups(ServerName, Username, 0, Flags, out bufPtr, 1024, out EntriesRead, out TotalEntries);
                //ErrorCode = api.NetUserGetLocalGroups(ServerName,Username,0,Flags,out bufPtr,1024,out EntriesRead, out TotalEntries);
                //if (ErrorCode==0) { _ErrorMessage="Successful"; }
                //else { _ErrorMessage="Username or computer not found"; }

                //if (Flags>1) _ErrorMessage="Flags can only be 0 or 1";

                if (EntriesRead > 0) {
                LOCALGROUP_USERS_INFO_0[] RetGroups = new LOCALGROUP_USERS_INFO_0[EntriesRead];
                IntPtr iter = bufPtr;
                for (Int64 i = 0; i < EntriesRead; i++) {
                    RetGroups[i] = (LOCALGROUP_USERS_INFO_0)Marshal.PtrToStructure(iter, typeof(LOCALGROUP_USERS_INFO_0));
                    iter = (IntPtr)((Int64)iter + (Int64)Marshal.SizeOf(typeof(LOCALGROUP_USERS_INFO_0)));
                    myList.Add(RetGroups[i].name);
                }

                api.NetApiBufferFree(bufPtr);
                }

                return myList;
            } //GetUserLocalGroups

            // Occurs on destruction of the Wrapper
            ~NetUtilWrapper() { Dispose(); }

            } // wrapper class
        } // namespace
        "@
        if ([IntPtr]::Size -eq 4) { $TypeDefinition=$TypeDefinition.Replace("Int64","Int32") }
        Add-Type -TypeDefinition $TypeDefinition
        $Netapi=New-Object Netapi32Wrapper.NetUtilWrapper
```
