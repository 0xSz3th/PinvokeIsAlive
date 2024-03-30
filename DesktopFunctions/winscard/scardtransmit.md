
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
  public struct SCARD_IO_REQUEST
  {
      public UInt32 dwProtocol;
      public UInt32 cbPciLength;
  }

[DllImport("winscard.dll")]
public static extern int SCardTransmit(
     IntPtr hCard, 
     ref SCARD_IO_REQUEST pioSendRequest, 
     ref byte SendBuff, 
     UInt32 SendBuffLen, 
     ref SCARD_IO_REQUEST pioRecvRequest,
     out byte RecvBuff, 
     ref UInt32 RecvBuffLen
);
```

## Tips & Tricks:
```cs
private int GetUID(ref byte[] UID)
    {
        byte[] receivedUID = new byte[10];
        UnsafeNativeMethods.SCARD_IO_REQUEST request = new UnsafeNativeMethods.SCARD_IO_REQUEST();
        request.dwProtocol = 1; //SCARD_PROTOCOL_T1);
        request.cbPciLength = System.Runtime.InteropServices.Marshal.SizeOf(typeof(UnsafeNativeMethods.SCARD_IO_REQUEST));
        byte[] sendBytes = new byte[] { 0xFF, 0xCA, 0x00, 0x00, 0x00 }; //get UID command for iClass cards

        int outBytes = receivedUID.Length;
        int status = SCardTransmit(_hCard, ref request, ref sendBytes[0], (uint)sendBytes.Length, ref request, out receivedUID[0], ref outBytes);

        UID = receivedUID.Take(8).ToArray(); //only take the first 8, the last 2 bytes are not part of the UID of the card (iClass 2k cards...not sure about others)
        return status;
    }
```

## Sample Code:
```cs
// Paste here code for SCardEstablishContext, SCardConnect

[DllImport("kernel32.dll", SetLastError=true)]
private extern static IntPtr LoadLibrary(string lpFileName);

[DllImport("kernel32.dll")]
private extern static void FreeLibrary(IntPtr handle) ;

[DllImport("kernel32.dll")]
private extern static IntPtr GetProcAddress(IntPtr handle, string
procName);

//Get the address of Pci from "Winscard.dll".
private static IntPtr GetPciT0()
{
IntPtr handle = LoadLibrary("Winscard.dll") ;
IntPtr pci = GetProcAddress(handle, "g_rgSCardT0Pci") ;
FreeLibrary(handle) ;
return pci ;
}

SCARD_IO_REQUEST ioRecv = new SCARD_IO_REQUEST();
byte[] pbRecvBuffer=new byte [255];
int pcbRecvLength=255;
byte[] pbSendBuffer = { 0xC0, 0xA4, 0x00, 0x00, 0x02, 0x3F, 0x00 }; // Example Cla,Ins,P1,P2,P3,DataIN (Select MF)
int cbSendLength=pbSendBuffer.Length;
ioRecv.cbPciLength = 255;
IntPtr SCARD_PCI_T0 = PCSC.GetPciT0();
uint errors=SCardTransmit(nCard, SCARD_PCI_T0, pbSendBuffer, cbSendLength, ioRecv, pbRecvBuffer, ref pcbRecvLength);

// Paste here code for SCardDisconnect, pbRecvBuffer contains Answer as Byte[]
```
