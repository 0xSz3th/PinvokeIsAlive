
## C# Signature:
```cs
/// <summary>
        /// The NetLocalGroupGetMembers function retrieves a list of the members of a particular local group in 
        /// the security database, which is the security accounts manager (SAM) database or, in the case 
        /// of domain controllers, the Active Directory. Local group members can be users or global groups.
        /// </summary>
        /// <param name="servername"></param>
        /// <param name="localgroupname"></param>
        /// <param name="level"></param>
        /// <param name="bufptr"></param>
        /// <param name="prefmaxlen"></param>
        /// <param name="entriesread"></param>
        /// <param name="totalentries"></param>
        /// <param name="resume_handle"></param>
        /// <returns></returns>
        [DllImport("NetAPI32.dll", CharSet=CharSet.Unicode)]
        public extern static int NetLocalGroupGetMembers(
            [MarshalAs(UnmanagedType.LPWStr)] string servername,
            [MarshalAs(UnmanagedType.LPWStr)] string localgroupname,
            int level,
            out IntPtr bufptr,
            int prefmaxlen,
            out int entriesread,
            out int totalentries,
            IntPtr resume_handle);
```

## VB Signature:
```cs
Declare Function NetLocalGroupGetMembers Lib "netapi32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Unicode)]
            public struct LOCALGROUP_MEMBERS_INFO_2 
        {
            public IntPtr lgrmi2_sid;
            public int lgrmi2_sidusage;
            public string lgrmi2_domainandname;
        }
```

## Sample Code:
```cs
//Example code for a class file or dll( I used a dll)
        public static ArrayList GetLocalGroupMembers(string ServerName,string GroupName)
        {
            ArrayList myList = new ArrayList();
            int EntriesRead;
            int TotalEntries;
            int Resume  = IntPtr.Zero;
            IntPtr buffer;
            int val = NetLocalGroupGetMembers(ServerName, GroupName, 2, out bufPtr, -1, out EntriesRead, out TotalEntries, Resume);
            if(EntriesRead> 0)
            {
                LOCALGROUP_MEMBERS_INFO_2[] Members = new LOCALGROUP_MEMBERS_INFO_2[EntriesRead];
                IntPtr iter = bufPtr;
                for(int i=0; i < EntriesRead; i++)
                {
                    Members[i] = (LOCALGROUP_MEMBERS_INFO_2)Marshal.PtrToStructure(iter, typeof(LOCALGROUP_MEMBERS_INFO_2)); 
                    iter = (IntPtr)((int)iter + Marshal.SizeOf(typeof(LOCALGROUP_MEMBERS_INFO_2)));
                    myList.Add(Members[i].lgrmi2_domainandname + "," + Members[i].lgrmi2_sidusage);
                }
                NetApiBufferFree(bufPtr);
            }
            return myList;
        }
```

## Sample Code:
```cs
//Example code for calling application
        ArrayList RetGroups = new ArrayList();
        RetGroups =DsDomain.GetLocalGroupMembers(null,"administrators");        
        string delimStr = ",";
        char [] delimiter = delimStr.ToCharArray();    
        foreach(string str in RetGroups)
    {        //I used this to retrieve the type of group so I could use an icon in a treeview if desired.
            //split[0] is the "domain\group or user", split[1] is the type, 1 for user, 2 for group.                
        string [] split = null;
        split = str.Split(delimiter);
        Console.WriteLine(split[0] + split[1]);
    }
```
