
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)] 
  private static extern Int32 LsaLookupSids( 
    IntPtr PolicyHandle, 
    int Count,
    IntPtr ptrEnumBuf, 
    out IntPtr ptrDomainList, 
    ref IntPtr ptrNameList);
```

## VB Signature:
```cs
Declare Auto Function LsaLookupSids Lib "advapi32.dll" (PolicyHandle As IntPtr, Count As Integer, ByRef Sids As IntPtr, ByRef ReferencedDomains As IntPtr, ByRef Names As IntPtr) As Integer
```

## User-Defined Types:
```cs
<StructLayout(LayoutKind.Sequential)>
    Structure LSA_REFERENCED_DOMAIN_LIST
    Public Entries As ULong
    Public Domains As LSA_TRUST_INFORMATION
    End Structure

    <StructLayout(LayoutKind.Sequential)>
    Structure LSA_TRUST_INFORMATION
    Public Name As LSA_UNICODE_STRING
    Public Sid As IntPtr
    End Structure

    <StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Unicode)>
    Structure LSA_UNICODE_STRING
    Public Length, MaximumLength As UShort
    <MarshalAs(UnmanagedType.LPWStr)> Public Buffer As String
    End Structure

    <StructLayout(LayoutKind.Sequential)>
    Structure LSA_TRANSLATED_NAME
    Public Use As SID_NAME_USE,
        Name As LSA_UNICODE_STRING,
        DomainIndex As Long
    End Structure

    Enum SID_NAME_USE
    SidTypeUser = 1
    SidTypeGroup
    SidTypeDomain
    SidTypeAlia
    SidTypeWellKnownGroup
    SidTypeDeletedAccount
    SidTypeInvalid
    SidTypeUnknown
    SidTypeComputer
    SidTypeLabel
    End Enum
```

## Sample Code:
```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace LsaSecurity
{
    /*
     * LsaWrapper class credit: Willy Denoyette [MVP]
     * 
     * http://www.hightechtalks.com/csharp/lsa-functions-276626.html
     * 
     * Added support for:
     * 
     *      LsaLookupSids
     * 
     * for the purposes of providing a working example.
     * 
     * 
     * 
     */


    using System.Runtime.InteropServices;
    using System.Security;
    using System.Management;
    using System.Runtime.CompilerServices;
    using System.ComponentModel;

    using LSA_HANDLE = IntPtr;

    public class Program
    {
    public static void Main()
    {
        using (LsaWrapper lsaSec = new LsaWrapper())
        {
        string[] accounts = lsaSec.GetUsersWithPrivilege("SeNetworkLogonRight");

        }

    }
    }
```

## Sample Code:
```cs
[StructLayout(LayoutKind.Sequential)]
    struct LSA_OBJECT_ATTRIBUTES
    {
    internal int Length;
    internal IntPtr RootDirectory;
    internal IntPtr ObjectName;
    internal int Attributes;
    internal IntPtr SecurityDescriptor;
    internal IntPtr SecurityQualityOfService;
    }
    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    struct LSA_UNICODE_STRING
    {
    internal ushort Length;
    internal ushort MaximumLength;
    [MarshalAs(UnmanagedType.LPWStr)]
    internal string Buffer;
    }

    sealed class Win32Sec
    {
    [DllImport("advapi32", CharSet = CharSet.Unicode, SetLastError = true),
    SuppressUnmanagedCodeSecurityAttribute]
    internal static extern uint LsaOpenPolicy(
    LSA_UNICODE_STRING[] SystemName,
    ref LSA_OBJECT_ATTRIBUTES ObjectAttributes,
    int AccessMask,
    out IntPtr PolicyHandle
    );

    [DllImport("advapi32", CharSet = CharSet.Unicode, SetLastError = true),
    SuppressUnmanagedCodeSecurityAttribute]
    internal static extern uint LsaAddAccountRights(
    LSA_HANDLE PolicyHandle,
    IntPtr pSID,
    LSA_UNICODE_STRING[] UserRights,
    int CountOfRights
    );

    [DllImport("advapi32", CharSet = CharSet.Unicode, SetLastError = true),
        SuppressUnmanagedCodeSecurityAttribute]
    internal static extern uint LsaRemoveAccountRights(
    LSA_HANDLE PolicyHandle,
    IntPtr pSID,
    bool allRights,
    LSA_UNICODE_STRING[] UserRights,
    int CountOfRights
    );

    [DllImport("advapi32", CharSet = CharSet.Unicode, SetLastError = true),
        SuppressUnmanagedCodeSecurityAttribute]
    internal static extern uint LsaEnumerateAccountsWithUserRight(
        LSA_HANDLE PolicyHandle,
        LSA_UNICODE_STRING[] UserRights,
        out IntPtr EnumerationBuffer,
        out int CountReturned
    );

    [DllImport("advapi32", CharSet = CharSet.Unicode, SetLastError = true),
    SuppressUnmanagedCodeSecurityAttribute]
    internal static extern uint LsaLookupSids(
        LSA_HANDLE PolicyHandle,
        int count,
        IntPtr buffer,
        out LSA_HANDLE domainList,
        out LSA_HANDLE nameList
    );
```

## Sample Code:
```cs
[DllImport("advapi32", CharSet = CharSet.Unicode, SetLastError = true),
    SuppressUnmanagedCodeSecurityAttribute]
    internal static extern int LsaLookupNames2(
    LSA_HANDLE PolicyHandle,
    uint Flags,
    uint Count,
    LSA_UNICODE_STRING[] Names,
    ref IntPtr ReferencedDomains,
    ref IntPtr Sids
    );
```

## Sample Code:
```cs
[DllImport("advapi32")]
    internal static extern int LsaNtStatusToWinError(int NTSTATUS);

    [DllImport("advapi32")]
    internal static extern int LsaClose(IntPtr PolicyHandle);

    [DllImport("advapi32")]
    internal static extern int LsaFreeMemory(IntPtr Buffer);

    }

    public sealed class LsaWrapper : IDisposable
    {
    private bool _writeToConsole = false;

    [StructLayout(LayoutKind.Sequential)]
    struct LSA_TRUST_INFORMATION
    {
        internal LSA_UNICODE_STRING Name;
        internal IntPtr Sid;
    }
    [StructLayout(LayoutKind.Sequential)]
    struct LSA_TRANSLATED_SID2
    {
        internal SidNameUse Use;
        internal IntPtr Sid;
        internal int DomainIndex;
        uint Flags;
    }

    //[StructLayout(LayoutKind.Sequential)]
    //struct LSA_REFERENCED_DOMAIN_LIST
    //{
    //    internal uint Entries;
    //    internal LSA_TRUST_INFORMATION Domains;
    //}
    // Commented by KaushalendraATgmail.com

    [StructLayout(LayoutKind.Sequential)]
    internal struct LSA_REFERENCED_DOMAIN_LIST
    {
        internal uint Entries;
        internal IntPtr Domains;
    }

    [StructLayout(LayoutKind.Sequential)]
    struct LSA_ENUMERATION_INFORMATION
    {
        internal LSA_HANDLE PSid;
    }

    [StructLayout(LayoutKind.Sequential)]
    struct LSA_SID
    {
        internal uint Sid;
    }

    [StructLayout(LayoutKind.Sequential)]
    struct LSA_TRANSLATED_NAME
    {
        internal SidNameUse Use;
        internal LSA_UNICODE_STRING Name;
        internal int DomainIndex;
    }

    enum SidNameUse : int
    {
        User = 1,
        Group = 2,
        Domain = 3,
        Alias = 4,
        KnownGroup = 5,
        DeletedAccount = 6,
        Invalid = 7,
        Unknown = 8,
        Computer = 9
    }

    enum Access : int
    {
        POLICY_READ = 0x20006,
        POLICY_ALL_ACCESS = 0x00F0FFF,
        POLICY_EXECUTE = 0X20801,
        POLICY_WRITE = 0X207F8
    }
    const uint STATUS_ACCESS_DENIED = 0xc0000022;
    const uint STATUS_INSUFFICIENT_RESOURCES = 0xc000009a;
    const uint STATUS_NO_MEMORY = 0xc0000017;

    IntPtr lsaHandle;

    public LsaWrapper()
        : this(null)
    { }
    // // local system if systemName is null
    public LsaWrapper(string systemName)
    {
        LSA_OBJECT_ATTRIBUTES lsaAttr;
        lsaAttr.RootDirectory = IntPtr.Zero;
        lsaAttr.ObjectName = IntPtr.Zero;
        lsaAttr.Attributes = 0;
        lsaAttr.SecurityDescriptor = IntPtr.Zero;
        lsaAttr.SecurityQualityOfService = IntPtr.Zero;
        lsaAttr.Length = Marshal.SizeOf(typeof(LSA_OBJECT_ATTRIBUTES));
        lsaHandle = IntPtr.Zero;
        LSA_UNICODE_STRING[] system = null;
        if (systemName != null)
        {
        system = new LSA_UNICODE_STRING[1];
        system[0] = InitLsaString(systemName);
        }

        uint ret = Win32Sec.LsaOpenPolicy(system, ref lsaAttr, (int)Access.POLICY_ALL_ACCESS, out lsaHandle);
        if (ret == 0)
        return;
        if (ret == STATUS_ACCESS_DENIED)
        {
        throw new UnauthorizedAccessException();
        }
        if ((ret == STATUS_INSUFFICIENT_RESOURCES) || (ret == STATUS_NO_MEMORY))
        {
        throw new OutOfMemoryException();
        }
        throw new Win32Exception(Win32Sec.LsaNtStatusToWinError((int)ret));
    }

    public string[] GetUsersWithPrivilege(string privilege)
    {
        LSA_UNICODE_STRING[] privileges = new LSA_UNICODE_STRING[1];
        privileges[0] = InitLsaString(privilege);

        IntPtr buffer;
        int count;
        uint ret =
        Win32Sec.LsaEnumerateAccountsWithUserRight(lsaHandle, privileges, out buffer, out count);

        if (ret != 0)
        {
        if (ret == STATUS_ACCESS_DENIED)
        {
            throw new UnauthorizedAccessException();
        }

        if (ret == STATUS_INSUFFICIENT_RESOURCES || ret == STATUS_NO_MEMORY)
        {
            throw new OutOfMemoryException();
        }

        throw new Win32Exception(Win32Sec.LsaNtStatusToWinError((int)ret));
        }

        LSA_ENUMERATION_INFORMATION[] lsaInfo = new LSA_ENUMERATION_INFORMATION[count];
        for (int i = 0, elemOffs = (int)buffer; i < count; i++)
        {
        lsaInfo[i] = (LSA_ENUMERATION_INFORMATION)Marshal.PtrToStructure((IntPtr)elemOffs, typeof(LSA_ENUMERATION_INFORMATION));
        elemOffs += Marshal.SizeOf(typeof(LSA_ENUMERATION_INFORMATION));
        }

        LSA_HANDLE domains;
        LSA_HANDLE names;
        ret = Win32Sec.LsaLookupSids(lsaHandle, lsaInfo.Length, buffer, out domains, out names);

        if (ret != 0)
        {
        if (ret == STATUS_ACCESS_DENIED)
        {
            throw new UnauthorizedAccessException();
        }

        if (ret == STATUS_INSUFFICIENT_RESOURCES || ret == STATUS_NO_MEMORY)
        {
            throw new OutOfMemoryException();
        }

        throw new Win32Exception(Win32Sec.LsaNtStatusToWinError((int)ret));
        }

        /*string[] retNames = new string[count];

        LSA_TRANSLATED_NAME[] lsaNames = new LSA_TRANSLATED_NAME[count];
        for (int i = 0, elemOffs = (int)names; i < count; i++)
        {
        lsaNames[i] = (LSA_TRANSLATED_NAME)Marshal.PtrToStructure((LSA_HANDLE)elemOffs, typeof(LSA_TRANSLATED_NAME));
        elemOffs += Marshal.SizeOf(typeof(LSA_TRANSLATED_NAME));

        LSA_UNICODE_STRING name = lsaNames[i].Name;
        retNames[i] = name.Buffer.Substring(0, name.Length / 2);
        }*/

        // Following code also fetches Domains and associates domains and usernames
        string[] retNames = new string[count];
        List<int> currentDomain = new List<int>();
        int domainCount = 0;

        LSA_TRANSLATED_NAME[] lsaNames = new LSA_TRANSLATED_NAME[count];
        for (int i = 0, elemOffs = (int)names; i < count; i++)
        {
        lsaNames[i] = (LSA_TRANSLATED_NAME)Marshal.PtrToStructure((LSA_HANDLE)elemOffs, typeof(LSA_TRANSLATED_NAME));
        elemOffs += Marshal.SizeOf(typeof(LSA_TRANSLATED_NAME));

        LSA_UNICODE_STRING name = lsaNames[i].Name;
        retNames[i] = name.Buffer.Substring(0, name.Length / 2);

        if (!currentDomain.Contains(lsaNames[i].DomainIndex))
        {
            domainCount = domainCount + 1;
            currentDomain.Add(lsaNames[i].DomainIndex);
        }
        //Error: not necessary to count domain names

        }

        string[] domainPtrNames = new string[count];

        LSA_REFERENCED_DOMAIN_LIST[] lsaDomainNames = new LSA_REFERENCED_DOMAIN_LIST[count];
        //Error: LSA_REFERENCED_DOMAIN_LIST is a structure, not an array

        for (int i = 0, elemOffs = (int)domains; i < count; i++)
        //Error: not necessary
        {
        lsaDomainNames[i] = (LSA_REFERENCED_DOMAIN_LIST)Marshal.PtrToStructure((LSA_HANDLE)elemOffs, typeof(LSA_REFERENCED_DOMAIN_LIST));
        elemOffs += Marshal.SizeOf(typeof(LSA_REFERENCED_DOMAIN_LIST));
        }

        LSA_TRUST_INFORMATION[] lsaDomainName = new LSA_TRUST_INFORMATION[count];
        string[] domainNames = new string[domainCount];

        for (int i = 0, elemOffs = (int)lsaDomainNames[i].Domains; i < domainCount; i++)
        {
        lsaDomainName[i] = (LSA_TRUST_INFORMATION)Marshal.PtrToStructure((LSA_HANDLE)elemOffs, typeof(LSA_TRUST_INFORMATION));
        elemOffs += Marshal.SizeOf(typeof(LSA_TRUST_INFORMATION));
```

## Sample Code:
```cs
LSA_UNICODE_STRING tempDomain = lsaDomainName[i].Name;
        //if(tempDomain.Buffer != null)
        //{
            domainNames[i] = tempDomain.Buffer.Substring(0, tempDomain.Length / 2);
        //}
        }

        string[] domainUserName = new string[count];

        for (int i = 0; i < lsaNames.Length; i++)
        {
        domainUserName[i] = domainNames[lsaNames[i].DomainIndex] + "\\" + retNames[i];
        }

        Win32Sec.LsaFreeMemory(buffer);
        Win32Sec.LsaFreeMemory(domains);
        Win32Sec.LsaFreeMemory(names);

        //return retNames;
        return domainUserName

    }

    public void AddPrivileges(string account, string privilege)
    {
        IntPtr pSid = GetSIDInformation(account);
        LSA_UNICODE_STRING[] privileges = new LSA_UNICODE_STRING[1];
        privileges[0] = InitLsaString(privilege);
        uint ret = Win32Sec.LsaAddAccountRights(lsaHandle, pSid, privileges, 1);

        if (ret == 0)
        {
        if (this._writeToConsole)
        {
            Console.WriteLine("Added: {0} to {1} successfully.", account, privilege);
        }
        return;
        }

        if (ret == STATUS_ACCESS_DENIED)
        {
        throw new UnauthorizedAccessException();
        }
        if ((ret == STATUS_INSUFFICIENT_RESOURCES) || (ret == STATUS_NO_MEMORY))
        {
        throw new OutOfMemoryException();
        }
        throw new Win32Exception(Win32Sec.LsaNtStatusToWinError((int)ret));
    }

    public void RemovePrivileges(string account, string privilege)
    {
        IntPtr pSid = GetSIDInformation(account);
        LSA_UNICODE_STRING[] privileges = new LSA_UNICODE_STRING[1];
        privileges[0] = InitLsaString(privilege);
        uint ret = Win32Sec.LsaRemoveAccountRights(lsaHandle, pSid, false, privileges, 1);

        if (ret == 0)
        {
        if (this._writeToConsole)
        {
            Console.WriteLine("Removed: {0} from {1} successfully.", account, privilege);
        }
        return;
        }
        if (ret == STATUS_ACCESS_DENIED)
        {
        throw new UnauthorizedAccessException();
        }
        if ((ret == STATUS_INSUFFICIENT_RESOURCES) || (ret == STATUS_NO_MEMORY))
        {
        throw new OutOfMemoryException();
        }
        throw new Win32Exception(Win32Sec.LsaNtStatusToWinError((int)ret));
    }
```

## Sample Code:
```cs
public void Dispose()
    {
        if (lsaHandle != IntPtr.Zero)
        {
        Win32Sec.LsaClose(lsaHandle);
        lsaHandle = IntPtr.Zero;
        }
        GC.SuppressFinalize(this);
    }
    ~LsaWrapper()
    {
        Dispose();
    }
    // helper functions

    IntPtr GetSIDInformation(string account)
    {
        LSA_UNICODE_STRING[] names = new LSA_UNICODE_STRING[1];
        LSA_TRANSLATED_SID2 lts;
        IntPtr tsids = IntPtr.Zero;
        IntPtr tdom = IntPtr.Zero;
        names[0] = InitLsaString(account);
        lts.Sid = IntPtr.Zero;
        int ret = Win32Sec.LsaLookupNames2(lsaHandle, 0, 1, names, ref tdom, ref tsids);
        if (ret != 0)
        throw new Win32Exception(Win32Sec.LsaNtStatusToWinError(ret));
        lts = (LSA_TRANSLATED_SID2)Marshal.PtrToStructure(tsids,
        typeof(LSA_TRANSLATED_SID2));
        Win32Sec.LsaFreeMemory(tsids);
        Win32Sec.LsaFreeMemory(tdom);
        return lts.Sid;
    }

    static LSA_UNICODE_STRING InitLsaString(string s)
    {
        // Unicode strings max. 32KB
        if (s.Length > 0x7ffe)
        throw new ArgumentException("String too long");
        LSA_UNICODE_STRING lus = new LSA_UNICODE_STRING();
        lus.Buffer = s;
        lus.Length = (ushort)(s.Length * sizeof(char));
        lus.MaximumLength = (ushort)(lus.Length + sizeof(char));

        // If unicode issues then do this instead of previous two line
        //lus.Length = (ushort)(s.Length * 2); // Unicode char is 2 bytes
        //lus.MaximumLength = (ushort)(lus.Length + 2)
```

## Sample Code:
```cs
return lus;
    }

    public bool WriteToConsole
    {
        set { this._writeToConsole = value; }
    }
    }
}
```
