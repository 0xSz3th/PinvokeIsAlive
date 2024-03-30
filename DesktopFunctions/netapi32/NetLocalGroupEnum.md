
## C# Signature:
```cs
[DllImport("Netapi32.dll")]
internal extern static int NetLocalGroupEnum([MarshalAs(UnmanagedType.LPWStr)] 
       string servername, 
       int level, 
       out IntPtr bufptr, 
       int prefmaxlen, 
       out int entriesread, 
       out int totalentries, 
       ref int resume_handle);
```

## VB Signature:
```cs
Declare Function NetLocalGroupEnum Lib "netapi32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
    internal struct LOCALGROUP_USERS_INFO_0
    {
        [MarshalAs(UnmanagedType.LPWStr)]internal string name;
    }
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    internal struct LOCALGROUP_USERS_INFO_1
    {
        [MarshalAs(UnmanagedType.LPWStr)] public string name;
        [MarshalAs(UnmanagedType.LPWStr)] public string comment;
    }
```

## Sample Code:
```cs
private string [] GetAllLocalGroups(string ServerName) {
            int size=1024;    //Start with 1k
            IntPtr bufptr=new IntPtr(size);
            int level=0;
            int prefmaxlen=1023;
            int entriesread=0;
            int totalentries=0;
            int resume_handle=0;
            int err=0;
            do
            {
                err= NativeMethods.NetLocalGroupEnum(
                    ServerName,
                    level,
                    out bufptr,
                    prefmaxlen,
                    out entriesread,
                    out totalentries,
                    ref resume_handle
                );
                switch(err)
                {
                    //If there is more data, double the size of the buffer...
                    case 2123:        //NERR_BufTooSmall
                    case 234:        //ERROR_MORE_DATA
                        size*=2;
                        bufptr=new IntPtr(size);
                        prefmaxlen=size-1;    //Increase the size you want read as well
                        resume_handle=0;    //And reset the resume_handle or you'll just pick up where you left off.

                        break;
                    case 2351:    //NERR_InvalidComputer
                    case 0:        //NERR_Success
                    default:
                        break;
                }
            }
            while(err==234);    // and start over

            LOCALGROUP_USERS_INFO_0 group=new LOCALGROUP_USERS_INFO_0(); //See user type above
            string [] ret = new string[totalentries];
            IntPtr iter = bufptr;

            for(int i=0; i < totalentries; i++)
            {
                group = (LOCALGROUP_USERS_INFO_0)Marshal.PtrToStructure(iter, typeof(LOCALGROUP_USERS_INFO_0));
                ret[i] = group.name;
                iter = (IntPtr)((int)iter + Marshal.SizeOf(typeof(LOCALGROUP_USERS_INFO_0)));
            }

            return ret;
        }
```

## Sample Code:
```cs
[DllImport("Netapi32.dll")]
        internal extern static int NetLocalGroupEnum(
            [MarshalAs(UnmanagedType.LPWStr)] string servername,
               int level,
               out IntPtr bufptr,
               int prefmaxlen,
               out int entriesread,
               out int totalentries,
               ref int resume_handle);

        [DllImport("Netapi32.dll")]
        internal extern static int NetApiBufferFree(IntPtr buffer);

        private static readonly int NERR_Success = 0;

        private static readonly int ERROR_ACCESS_DENIED = 5;
        private static readonly int ERROR_MORE_DATA = 234;
        private static readonly int NERR_Base = 2100;
        private static readonly int NERR_InvalidComputer = NERR_Base + 251;
        private static readonly int NERR_BufTooSmall = NERR_Base + 23;
```

## Sample Code:
```cs
public static LOCALGROUP_USERS_INFO_1[] GetAllLocalGroups()
        {
            return GetAllLocalGroups(null);
        }

        public static LOCALGROUP_USERS_INFO_1[] GetAllLocalGroups(string serverName)
        {
            int res = 0;
            int level = 1;
            IntPtr buffer = IntPtr.Zero;
            int MAX_PREFERRED_LENGTH = -1;
            int read, total;
            int handle = 0;

            var groups = new List<LOCALGROUP_USERS_INFO_1>();
            try
            {
                res = NetLocalGroupEnum(serverName, level, out buffer, MAX_PREFERRED_LENGTH,
                    out read, out total, ref handle);

                if (res != NERR_Success)
                {
                    DumpError(res);
                    return groups.ToArray();
                }

                IntPtr ptr = buffer;
                for (int i = 0; i < read; i++)
                {
                    var group = (LOCALGROUP_USERS_INFO_1)Marshal.PtrToStructure(ptr, typeof(LOCALGROUP_USERS_INFO_1));
                    groups.Add(group);
                    ptr = (IntPtr)((int)ptr + Marshal.SizeOf(typeof(LOCALGROUP_USERS_INFO_1)));
                }
            }
            finally
            {
                NetApiBufferFree(buffer);
            }

            return groups.ToArray();
        }

        private static void DumpError(int res)
        {
            if(res == ERROR_ACCESS_DENIED)
                Trace.WriteLine("ERROR_ACCESS_DENIED");
            else if(res == ERROR_MORE_DATA)
                    Trace.WriteLine("ERROR_MORE_DATA");
            else if(res == NERR_InvalidComputer)
                    Trace.WriteLine("NERR_InvalidComputer");
            else if(res == NERR_BufTooSmall)
                    Trace.WriteLine("NERR_BufTooSmall");
            else
                Trace.WriteLine("Error 0x" + res.ToString("x"));
        }
```
