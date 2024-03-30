
## C# Signature:
```cs
[DllImport("Eappcfg.dll", SetLastError=true)]
private static unsafe extern UInt32 EapHostPeerInvokeConfigUI(IntPtr handle, uint dwflags, EAP_METHOD_TYPE eapMethodType, uint dwSizeOfConfigIn, byte *pConfigIn, uint *pdwSizeOfConfigOut, byte **ppConfigOut, ref IntPtr error);
```

## VB Signature:
```cs
Declare Function EapHostPeerInvokeConfigUI Lib "wlanapi.dll" (TODO) As TODO
```

## Sample Code:
```cs
eapType = new EAP_TYPE   {
                                dwVendorId = 0,
                                dwVendorType = 0,
                                type = typeval/* EAP method for PEAP */
                                },
                         dwAuthorId = 0
                              };
        unsafe
        {
        byte *connectionData = null;
        uint sizeConnectionData = 0;
        IntPtr er=IntPtr.Zero;
        UInt32 result = EapHostPeerInvokeConfigUI(handle, 0, method, 0, null, &sizeConnectionData, &connectionData, ref er);
        MessageBox.Show(sizeConnectionData+"jfdgkj");
        output = new byte[sizeConnectionData];
        for (int i = 0; i < sizeConnectionData; i++)
        {
            output[i] = *connectionData;
            //MessageBox.Show(*connectionData+" value"+i);
            connectionData++;

        }
```
