
## C# Signature:
```cs
[DllImport("advapi32", CharSet = CharSet.Unicode, SetLastError = true)]
    static extern uint LsaEnumerateAccountsWithUserRight(
    LSA_HANDLE PolicyHandle,
    LSA_UNICODE_STRING[] UserRights,
    out IntPtr EnumerationBuffer,
    out int CountReturned);
```

## VB Signature:
```cs
Declare Function LsaEnumerateAccountsWithUserRight Lib "advapi32.dll" ( _
    ByVal PolicyHandle As IntPtr, _
    ByRef userRights As LSA_UNICODE_STRING, _
    ByRef EnumerationBuffer As IntPtr, _
    ByRef CountReturned As Integer _
    ) As Integer
```

## Notes:
```cs
'NTSTATUS LsaEnumerateAccountsWithUserRight(
    '  LSA_HANDLE PolicyHandle,
    '  PLSA_UNICODE_STRING UserRights,
    '  PVOID* EnumerationBuffer,
    '  PULONG CountReturned
    ');
```

## C#.Net Sample Code:
```cs
using System;
using System.Runtime.InteropServices;
using System.Security;
using System.ComponentModel;

namespace LsaSecurity
{
    using LSA_HANDLE = IntPtr;

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

    [StructLayout(LayoutKind.Sequential)]
    struct LSA_ENUMERATION_INFORMATION
    {
    internal IntPtr PSid;
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
    internal static extern uint LsaEnumerateAccountsWithUserRight(
    LSA_HANDLE PolicyHandle,
    LSA_UNICODE_STRING[] UserRights,
    out IntPtr EnumerationBuffer,
    out int CountReturned
    );

    [DllImport("advapi32")]
    internal static extern int LsaNtStatusToWinError(int NTSTATUS);

    [DllImport("advapi32")]
    internal static extern int LsaClose(IntPtr PolicyHandle);

    [DllImport("advapi32")]
    internal static extern int LsaFreeMemory(IntPtr Buffer);

    }
    public class LsaWrapper : IDisposable
    {
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
    const uint STATUS_NO_MORE_ENTRIES = 0xc000001A;

    IntPtr lsaHandle;

    public LsaWrapper()
        : this(null)
    { }
    // local system if systemName is null
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

        uint ret = Win32Sec.LsaOpenPolicy(system, ref lsaAttr,
        (int)Access.POLICY_ALL_ACCESS, out lsaHandle);
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

    public void ReadPrivilege(string privilege)
    {
        LSA_UNICODE_STRING[] privileges = new LSA_UNICODE_STRING[1];
        privileges[0] = InitLsaString(privilege);
        IntPtr buffer;
        int count = 0;
        uint ret = Win32Sec.LsaEnumerateAccountsWithUserRight(lsaHandle, privileges, out buffer, out count);
        if (ret == 0)
        {

        LSA_ENUMERATION_INFORMATION[] LsaInfo = new LSA_ENUMERATION_INFORMATION[count];

        for (int i = 0, elemOffs = (int)buffer; i < count; i++)
        {
            LsaInfo[i] = (LSA_ENUMERATION_INFORMATION)Marshal.PtrToStructure(
                   (IntPtr)elemOffs, typeof(LSA_ENUMERATION_INFORMATION));

            elemOffs += Marshal.SizeOf(typeof(LSA_ENUMERATION_INFORMATION));
        }

        // Do something with LsaInfo here
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

    static LSA_UNICODE_STRING InitLsaString(string s)
    {
        // Unicode strings max. 32KB
        if (s.Length > 0x7ffe)
        throw new ArgumentException("String too long");
        LSA_UNICODE_STRING lus = new LSA_UNICODE_STRING();
        lus.Buffer = s;
        lus.Length = (ushort)(s.Length * sizeof(char));
        lus.MaximumLength = (ushort)(lus.Length + sizeof(char));
        return lus;
    }
    }

    class Program
    {
    static void Main(string[] args)
    {
        using (LsaSecurity.LsaWrapper lsa = new LsaSecurity.LsaWrapper())
        {
        lsa.ReadPrivilege("SeBatchLogonRight");
        }
    }
    }
}
```

## VB.Net Sample Code:
```cs
Private WinWorldSid As Integer = 1
    Private POLICY_ALL_ACCESS As Integer = &HF0FFF
    Private SECURITY_MAX_SID_SIZE As Integer = 68
    Private SE_DENY_REMOTE_INTERACTIVE_LOGON_NAME As String = "SeDenyRemoteInteractiveLogonRight"
    Private NT_STATUS_OBJECT_NAME_NOT_FOUND As Integer = &HC0000034
    Private STATUS_NO_MORE_ENTRIES As Integer = &H8000001A

    ' Check to see if the Deny permission already exists
    Public Function CheckTS(ByVal PC As String) As Boolean
    Dim ret, Access, sidsize, count, i As Integer
    Dim SystemName, DenyTSRights As LSA_UNICODE_STRING
    Dim ObjectAttr As LSA_OBJECT_ATTRIBUTES
    Dim Policy, EveryoneSID, EnumBuf, ptr As IntPtr
    Dim LsaInfo As LSA_ENUMERATION_INFORMATION
    Dim ans As Boolean

    ' build a well-known SID for "Everyone"
    sidsize = SECURITY_MAX_SID_SIZE
    EveryoneSID = Marshal.AllocHGlobal(sidsize)
    If CreateWellKnownSid(WinWorldSid, IntPtr.Zero, EveryoneSID, sidsize) = False Then
        ret = Marshal.GetLastWin32Error()
        Throw New Win32Exception(ret)
    End If

    ' setup the parameters for the LsaOpenPolicy API
    ObjectAttr.Length = Marshal.SizeOf(ObjectAttr)
    SystemName.Length = PC.Length * UnicodeEncoding.CharSize
    SystemName.MaximumLength = (PC.Length + 1) * UnicodeEncoding.CharSize
    SystemName.Buffer = Marshal.StringToHGlobalUni(PC)
    Access = POLICY_ALL_ACCESS

    ' open a policy handle on the remote PC
    ret = LsaOpenPolicy(SystemName, ObjectAttr, Access, Policy)
    If ret <> 0 Then
        Throw New Win32Exception(LsaNtStatusToWinError(ret))
    End If

    ' clean up
    Marshal.FreeHGlobal(SystemName.Buffer)

    ' Setup the input parameters for the LsaEnumerateAccountsWithUserRight API
    DenyTSRights.Length = SE_DENY_REMOTE_INTERACTIVE_LOGON_NAME.Length * UnicodeEncoding.CharSize
    DenyTSRights.MaximumLength = (SE_DENY_REMOTE_INTERACTIVE_LOGON_NAME.Length + 1) * UnicodeEncoding.CharSize
    DenyTSRights.Buffer = Marshal.StringToHGlobalUni(SE_DENY_REMOTE_INTERACTIVE_LOGON_NAME)

    ' do it!
    ret = LsaEnumerateAccountsWithUserRight(Policy, DenyTSRights, EnumBuf, count)
    If ret <> 0 Then
        Marshal.FreeHGlobal(DenyTSRights.Buffer)
        LsaClose(Policy)
        ' if there are no matching entries
        If ret = STATUS_NO_MORE_ENTRIES Then
        Return False
        End If
        Throw New Win32Exception(LsaNtStatusToWinError(ret))
    End If

    ' check to see if the Everyone SID is currently in the list
    ans = False
    For i = 0 To count - 1
        ptr = New IntPtr(EnumBuf.ToInt32 + (i * Marshal.SizeOf(LsaInfo)))
        LsaInfo = CType(Marshal.PtrToStructure(ptr, GetType(LSA_ENUMERATION_INFORMATION)), LSA_ENUMERATION_INFORMATION)
        If EqualSid(LsaInfo.Sid, EveryoneSID) Then
        ans = True
        Exit For
        End If
    Next

    ' clean up
    LsaFreeMemory(EnumBuf)
    Marshal.FreeHGlobal(DenyTSRights.Buffer)
    LsaClose(Policy)

    Return ans
    End Function
```
