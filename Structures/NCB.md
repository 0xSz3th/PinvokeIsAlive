
## C# Definition:
```cs
public static const int NCBNAMSZ=16;
    [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
    public struct NCB
    {
        byte ncb_command;
        byte ncb_retcode;
        byte ncb_lsn;
        byte ncb_num;
        IntPtr ncb_buffer;
        short ncb_length;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst=NetbiosConstants.NCBNAMSZ)]
        String ncb_callname;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst=NetbiosConstants.NCBNAMSZ)]
        String ncb_name;
        byte ncb_rto;
        byte ncb_sto;
        IntPtr ncb_post;
        byte ncb_lana_num;
        byte ncb_cmd_cplt;
        [MarshalAs(UnmanagedType.ByValArray, SizeConst=10)]
        byte[] ncb_reserve;
        IntPtr ncb_event;
    }

!!!!VB Definition:
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

## Notes:
```cs
Typedef struct _NCB {
   UCHAR   ncb_command;        /* command code           */
   UCHAR   ncb_retcode;        /* return code            */
   UCHAR   ncb_lsn;        /* local session number       */
   UCHAR   ncb_num;        /* number of our network name     */
   PUCHAR  ncb_buffer;         /* address of message buffer      */
   WORD    ncb_length;         /* size of message buffer     */
   UCHAR   ncb_callname[NCBNAMSZ]; /* blank-padded name of remote    */
   UCHAR   ncb_name[NCBNAMSZ];     /* our blank-padded netname       */
   UCHAR   ncb_rto;        /* rcv timeout/retry count    */
   UCHAR   ncb_sto;        /* send timeout/sys timeout       */
   void (CALLBACK *ncb_post)( struct _NCB * ); /* POST routine address    */
   UCHAR   ncb_lana_num;       /* lana (adapter) number      */
   UCHAR   ncb_cmd_cplt;       /* 0xff => commmand pending       */
#ifdef _WIN64
   UCHAR   ncb_reserve[18];    /* reserved, used by BIOS     */
#else
   UCHAR   ncb_reserve[10];    /* reserved, used by BIOS     */
#End If
   HANDLE  ncb_event;          /* HANDLE to Win32 event which    */
                   /* will be set to the signalled   */
                   /* state when an ASYNCH command   */
                   /* completes              */
} NCB, *PNCB;
```
