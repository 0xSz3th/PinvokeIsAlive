
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
internal struct ADAPTER_STATUS
    {
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 6)]
    byte[] adapter_address;
    byte rev_major;
    byte reserved0;
    byte adapter_type;
    byte rev_minor;
    short duration;
    short frmr_recv;
    short frmr_xmit;
    short iframe_recv_err;
    short xmit_aborts;
    int xmit_success;
    int recv_success;
    short iframe_xmit_err;
    short recv_buff_unavail;
    short t1_timeouts;
    short ti_timeouts;
    int Reserved1;
    short free_ncbs;
    short max_cfg_ncbs;
    short max_ncbs;
    short xmit_buf_unavail;
    short max_dgram_size;
    short pending_sess;
    short max_cfg_sess;
    short max_sess;
    short max_sess_pkt_size;
    short name_count;
    }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Private Structure ADAPTER_STATUS
   <MarshalAs(UnmanagedType.ByValArray, SizeConst:=6)> Dim adapter_address() As Byte
   Dim rev_major As Byte
   Dim reserved0 As Byte
   Dim adapter_type As Byte
   Dim rev_minor As Byte
   Dim duration As Short
   Dim frmr_recv As Short
   Dim frmr_xmit As Short
   Dim iframe_recv_err As Short
   Dim xmit_aborts As Short
   Dim xmit_success As Integer
   Dim recv_success As Integer
   Dim iframe_xmit_err As Short
   Dim recv_buff_unavail As Short
   Dim t1_timeouts As Short
   Dim ti_timeouts As Short
   Dim Reserved1 As Integer
   Dim free_ncbs As Short
   Dim max_cfg_ncbs As Short
   Dim max_ncbs As Short
   Dim xmit_buf_unavail As Short
   Dim max_dgram_size As Short
   Dim pending_sess As Short
   Dim max_cfg_sess As Short
   Dim max_sess As Short
   Dim max_sess_pkt_size As Short
   Dim name_count As Short
End Structure
```

## Notes:
```cs
typedef struct _ADAPTER_STATUS { 
   UCHAR   adapter_address[6]; 
   UCHAR   rev_major; 
   UCHAR   reserved0; 
   UCHAR   adapter_type; 
   UCHAR   rev_minor; 
   WORD    duration; 
   WORD    frmr_recv; 
   WORD    frmr_xmit; 
   WORD    iframe_recv_err; 
   WORD    xmit_aborts; 
   DWORD   xmit_success; 
   DWORD   recv_success; 
   WORD    iframe_xmit_err; 
   WORD    recv_buff_unavail; 
   WORD    t1_timeouts; 
   WORD    ti_timeouts; 
   DWORD   reserved1; 
   WORD    free_ncbs; 
   WORD    max_cfg_ncbs; 
   WORD    max_ncbs; 
   WORD    xmit_buf_unavail; 
   WORD    max_dgram_size; 
   WORD    pending_sess; 
   WORD    max_cfg_sess; 
   WORD    max_sess; 
   WORD    max_sess_pkt_size; 
   WORD    name_count; 
} ADAPTER_STATUS, *PADAPTER_STATUS;
```
