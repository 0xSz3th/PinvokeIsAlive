
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
public struct _NCB 
{
    public Commands ncb_command;      /* command code           */
    public byte   ncb_retcode;        /* return code            */
    public byte   ncb_lsn;        /* local session number       */
    public byte   ncb_num;        /* number of our network name     */
    //[MarshalAs(UnmanagedType.ByValArray, SizeConst = NCBNAMSZ)]
    //[MarshalAs(UnmanagedType.LPStr)]
    //[MarshalAs(UnmanagedType.LPArray)]
    public IntPtr ncb_buffer;         /* address of message buffer      */
    public ushort ncb_length;         /* size of message buffer     */
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = NativeMethods.NCBNAMSZ)]
    public byte[]   ncb_callname; /* blank-padded name of remote    */
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = NativeMethods.NCBNAMSZ)]
    public byte[]   ncb_name;         /* our blank-padded netname       */
    public byte   ncb_rto;        /* rcv timeout/retry count    */
    public byte   ncb_sto;        /* send timeout/sys timeout       */
    public IntPtr postroutine;//void (CALLBACK *ncb_post)( struct _NCB * ); /* POST routine address    */
    public byte   ncb_lana_num;       /* lana (adapter) number      */
    public byte   ncb_cmd_cplt;       /* 0xff => commmand pending       */
    [MarshalAs(UnmanagedType.LPArray, SizeConst=10)]
    public byte[/*10*/]   ncb_reserve;    /* reserved, used by BIOS     */
    public IntPtr  ncb_event;         /* HANDLE to Win32 event which    */
                    /* will be set to the signalled   */
                    /* state when an ASYNCH command   */
                    /* completes              */
}

[DllImport("netapi32.dll", SetLastError=true)]
static extern byte Netbios(ref _NCB controlBlock);
```

## VB Signature:
```cs
Private Declare Function Netbios Lib "netapi32.dll" ( _
   ByRef pncb As NCB _
) As Byte
```

## User-Defined Types:
```cs
Private Const NCBNAMSZ As Integer = 16

<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Ansi)> _
Private Structure NCB
   Dim ncb_command As Byte
   Dim ncb_retcode As Byte
   Dim ncb_lsn As Byte
   Dim ncb_num As Byte
   Dim ncb_buffer As IntPtr
   Dim ncb_length As Short
   <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=NCBNAMSZ)> Dim ncb_callname As String
   <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=NCBNAMSZ)> Dim ncb_name As String
   Dim ncb_rto As Byte
   Dim ncb_sto As Byte
   Dim ncb_post As IntPtr
   Dim ncb_lana_num As Byte
   Dim ncb_cmd_cplt As Byte
   <MarshalAs(UnmanagedType.ByValArray, SizeConst:=10)> Dim ncb_reserve() As Byte
   Dim ncb_event As IntPtr
End Structure
```

## VB.Net Sample Code:
```cs
Private Const NCBNAMSZ As Integer = 16
Private Const MAX_LANA As Integer = 254
Private Const NCBRESET As Integer = &H32
Private Const NCBASTAT As Integer = &H33
Private Const NCBENUM As Integer = &H37

<StructLayout(LayoutKind.Sequential)> _
Private Structure ASTAT
   Dim adapt As ADAPTER_STATUS
    <MarshalAs(UnmanagedType.ByValArray, SizeConst:=30)> Dim NameBuff() As NAME_BUFFER
End Structure

' Get the MAC Address of a remote PC
Function GetMACAddress(ByVal RemoteIP As String) As String
   Dim sb As New StringBuilder
   Dim myNcb As New NCB
   Dim myAdapt As New ADAPTER_STATUS
   Dim myASTAT As New ASTAT
   Dim myLana As New LANA_ENUM
   Dim ptr As IntPtr
   Dim i As Integer
   Dim bRet, FirstLANA As Byte

   ' First, we'll need to discover which LANA number is being used.
   ' So, we create a LANA_ENUM buffer (with a bit of pointer magic)
   ptr = Marshal.AllocHGlobal(Marshal.SizeOf(myLana))
   Marshal.StructureToPtr(myLana, ptr, False)

   ' load the NCB
   myNcb.ncb_command = NCBENUM
   myNcb.ncb_length = CShort(Marshal.SizeOf(myLana))
   myNcb.ncb_buffer = ptr

   ' execute the NetBIOS command
   bRet = Netbios(myNcb)
   If bRet <> 0 Then
     Marshal.FreeHGlobal(ptr)
     Throw New ApplicationException("Can't get the list of LANAs, error code=" & bRet)
     Return Nothing
   End If

   ' cast it back with pointer magic
   myLana = CType(Marshal.PtrToStructure(ptr, GetType(LANA_ENUM)), LANA_ENUM)
   FirstLANA = myLana.lana(0)

   ' Next we do a "reset" on the NetBIOS interface
   myNcb.ncb_command = NCBRESET
   myNcb.ncb_lana_num = FirstLANA

   ' execute the NetBIOS command
   bRet = Netbios(myNcb)
   If bRet <> 0 Then
     Marshal.FreeHGlobal(ptr)
     Throw New ApplicationException("Can't Reset the NetBIOS interface, error code=" & bRet)
     Return Nothing
   End If

   ' Create an Adapater Status packet (with more pointer magic)
   Marshal.FreeHGlobal(ptr)
   myASTAT.adapt = myAdapt
   ptr = Marshal.AllocHGlobal(Marshal.SizeOf(myASTAT))
   Marshal.StructureToPtr(myASTAT, ptr, False)

   ' Now we load up our adapter request
   myNcb.ncb_command = NCBASTAT
   myNcb.ncb_lana_num = FirstLANA
   myNcb.ncb_callname = RemoteIP.PadRight(NCBNAMSZ, " "c)
   myNcb.ncb_buffer = ptr
   myNcb.ncb_length = CShort(Marshal.SizeOf(myASTAT))

   ' execute the NetBIOS command
   bRet = Netbios(myNcb)
   If bRet <> 0 Then
     Marshal.FreeHGlobal(ptr)
     Throw New ApplicationException("Can't get the Adapter Status, error code=" & bRet)
     Return Nothing
   End If

   ' cast it back with pointer magic
   myASTAT = CType(Marshal.PtrToStructure(ptr, GetType(ASTAT)), ASTAT)

   ' make a string version of the MAC address
   For i = 0 To 5
     sb.AppendFormat("{0:X2}:", myASTAT.adapt.adapter_address(i))
   Next

   Marshal.FreeHGlobal(ptr)
   Return sb.ToString.TrimEnd(":"c)
End Function
```

## Alternative Managed API:
```cs
'-----------------------------------------------------------
  ' NetBIOS Network Control Block structure--which is used to
  ' issue all commands to the NetBIOS protocol
  '-----------------------------------------------------------
  Public Enum netbstrcs
    netNameLen = 16                  '[Length if name in bytes]
    netresvLen = 11                  '[Length of reserve array]
    netbuffer = 32000              '[Total size of data butter]
    netnumSess = 10              '[Total number of active sessions]
    netMAC = 7                       '[MAC address len]
    netnumNames = 17        '[Number of netbios names in adapter table]
  End Enum

  <StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Unicode)> _
  Public Structure NCB
    <MarshalAs(UnmanagedType.U1)> _
    Public ncbCommand As Byte
    <MarshalAs(UnmanagedType.U1)> _
    Public ncbRetcode As Byte
    <MarshalAs(UnmanagedType.U1)> _
    Public ncbLSN As Byte
    <MarshalAs(UnmanagedType.U1)> _
    Public ncbNum As Byte
    <MarshalAs(UnmanagedType.SysUInt)> _
    Public ncbBuffer As IntPtr
    <MarshalAs(UnmanagedType.U2)> _
    Public ncbLength As Int16
    <MarshalAs(UnmanagedType.ByValArray, ArraySubType:=UnmanagedType.U1, _
           SizeConst:=netbstrcs.netNameLen)> Dim ncbCallname() As Byte
    <MarshalAs(UnmanagedType.ByValArray, ArraySubType:=UnmanagedType.U1, _
           SizeConst:=netbstrcs.netNameLen)> Dim ncbName() As Byte
    <MarshalAs(UnmanagedType.U1)> _
    Public ncbRTO As Byte
    <MarshalAs(UnmanagedType.U1)> _
    Public ncbSTO As Byte
    <MarshalAs(UnmanagedType.U4)> _
    Public ncbPost As UInt32 'IntPtr
    <MarshalAs(UnmanagedType.U1)> _
    Public ncbLANAnum As Byte
    <MarshalAs(UnmanagedType.U1)> _
    Public ncbCmdCplt As Byte
    <MarshalAs(UnmanagedType.ByValArray, ArraySubType:=UnmanagedType.U1, _
           SizeConst:=netbstrcs.netresvLen)> Dim ncbReserve() As Byte
    <MarshalAs(UnmanagedType.U4)> _
    Public ncbEvent As Int32 'IntPtr
  End Structure
```
