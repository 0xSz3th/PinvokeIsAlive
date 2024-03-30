
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
static extern bool ConvertStringSidToSid(
            string StringSid,
            out IntPtr ptrSid
            );
```

## VB Signature:
```cs
Private Declare Auto Function ConvertStringSidToSid Lib "advapi32.dll" (StringSid As String, ByRef ptrSid As IntPtr) As Boolean
```

## C#.Net Sample Code:
```cs
ManagementBaseObject Descriptor = null;
    ManagementObjectCollection UserSearch = new ManagementObjectSearcher("Select * From Win32_LogicalFileSecuritySetting Where Path='" + FromPath + "'").Get();
    try
    {
        foreach(ManagementObject UserObject in UserSearch)
        { 
            ManagementBaseObject inParams1 = UserObject.GetMethodParameters("GetSecurityDescriptor"); 
            ManagementBaseObject outParams1 = UserObject.InvokeMethod("GetSecurityDescriptor", inParams1, null); 
            Descriptor = ((ManagementBaseObject)(outParams1.Properties["Descriptor"].Value)); 
        }
    }
    catch (Exception se)
    {
        Trace.WriteLine(se.Message);
    }

    ManagementObject Share = new ManagementObject("Win32_Directory='" + ToPath + "'"); 
    ManagementBaseObject inParams = Share.GetMethodParameters("ChangeSecurityPermissions"); 

    inParams["Option"] = 4; 
    inParams["SecurityDescriptor"] = Descriptor; 

    ManagementBaseObject outParams = Share.InvokeMethod("ChangeSecurityPermissions", inParams, null);
```

## C#.Net Sample Code:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
    static extern bool ConvertStringSidToSid(
        string lbBuffer, 
        out IntPtr ptrSid); 

    [DllImport("advapi32.dll", EntryPoint = "GetLengthSid", CharSet = CharSet.Auto)]
    static extern int GetLengthSid(IntPtr pSID);

    #region AccessMask 
    public class AccessMask
    { 
        public static uint FullAccess = 0x1F01FF; 
        public static uint FILE_LIST_DIRECTORY = 0x1; 
        public static uint FILE_ADD_FILE = 0x2;
        public static uint FILE_ADD_SUBDIRECTORY = 0x4;
        public static uint FILE_READ_EA = 0x8;
        public static uint FILE_WRITE_EA = 0x10;
        public static uint FILE_TRAVERSE = 0x20;
        public static uint FILE_DELETE_CHILD = 0x40;
        public static uint FILE_READ_ATTRIBUTES = 0x80;
        public static uint FILE_WRITE_ATTRIBUTES = 0x100;
        public static uint DELETE  = 0x10000;
        public static uint READ_CONTROL = 0x20000;
        public static uint WRITE_DAC = 0x40000;
        public static uint WRITE_OWNER = 0x80000;
        public static uint SYNCHRONIZE = 0x100000; 
    } 
    #endregion 
    #region AceFlags 
    public class AceFlags
    { 
        public static uint OBJECT_INHERIT_ACE = 0x1;
        public static uint CONTAINER_INHERIT_ACE = 0x2;
        public static uint NO_PROPAGATE_INHERIT_ACE = 0x4;
        public static uint INHERIT_ONLY_ACE = 0x8;
        public static uint INHERITED_ACE = 0x10; 
        public static uint SUCCESSFUL_ACCESS_ACE_FLAG = 0x40; 
        public static uint FAILED_ACCESS_ACE_FLAG = 0x80; 
    } 
    #endregion 
    #region AceType 
    public class AceType
    { 
        public static uint ACCESS_ALLOWED_ACE = 0; 
        public static uint ACCESS_DENIED_ACE = 1; 
        public static uint AUDIT_ACE = 2; 
    } 
    #endregion 
            #region SecurtyDescriptor 
    public class ControlFlags
    { 
        public static uint SE_OWNER_DEFAULTED = 0x1;
        public static uint SE_GROUP_DEFAULTED = 0x2;
        public static uint SE_DACL_PRESENT = 0x4;
        public static uint SE_DACL_DEFAULTED = 0x8;
        public static uint SE_SACL_PRESENT = 0x10;
        public static uint SE_SACL_DEFAULTED = 0x20;
        public static uint SE_DACL_AUTO_INHERIT_REQ = 0x100;
        public static uint SE_SACL_AUTO_INHERIT_REQ = 0x200;
        public static uint SE_DACL_AUTO_INHERITED = 0x400;
        public static uint SE_SACL_AUTO_INHERITED = 0x800;
        public static uint SE_DACL_PROTECTED = 0x1000;
        public static uint SE_SACL_PROTECTED = 0x2000;
        public static uint SE_SELF_RELATIVE = 0x8000; 
    } 
    #endregion 

    public static ManagementObject GetInstance(string Account, uint 
        AccessMask, uint AceType, uint AceFlags)
    { 
        ManagementObject Ace = new 
            System.Management.ManagementClass("Win32_Ace").CreateInstance(); 
        Ace["Trustee"] = Win32_Trustee(Account); 
        Ace["AccessMask"] = AccessMask; 
        Ace["AceType"] = AceType;
        Ace["AceFlags"] = AceFlags; 
        return Ace; 
    } 

    private static ManagementObject Win32_Trustee(string Account)
    { 
        byte[] SID = null; 
        ManagementObjectCollection UserSearch = 
            new ManagementObjectSearcher("Select * From Win32_Account Where Name = '" + Account + "'").Get();
        try
        {
            foreach(ManagementObject UserObject in UserSearch)
            { 
                IntPtr SID_ptr=new IntPtr(0); 
                ConvertStringSidToSid(UserObject["SID"].ToString(), out SID_ptr); 
                int size = (int)GetLengthSid(SID_ptr);
                SID = new byte[size]; 
                Marshal.Copy(SID_ptr, SID, 0, size); 
                Marshal.FreeHGlobal(SID_ptr);
            }
        }
        catch (Exception se)
        {
            Trace.WriteLine(se.Message);
        }
        ManagementObject Trustee = new System.Management.ManagementClass("Win32_Trustee").CreateInstance(); 
        Trustee["SID"] = SID; 
        return Trustee; 
    }
```
