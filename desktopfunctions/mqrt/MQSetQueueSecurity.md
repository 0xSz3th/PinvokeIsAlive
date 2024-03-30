
## C# Signature:
```cs
[DllImport("mqrt.dll", SetLastError=false, CharSet=CharSet.Auto)]
public static extern uint MQSetQueueSecurity(
      [MarshalAs(UnmanagedType.LPWStr)]
      string lpwcsFormatName
    , int SecurityInformation
    , IntPtr pSecurityDescriptor
);
```

## VB Signature:
```cs
Declare Function MQSetQueueSecurity Lib "mqrt.dll" (TODO) As TODO
```

## Sample Code:
```cs
class mqrt {

        public const int OWNER_SECURITY_INFORMATION = 0x1;
        public const int MQ_OK = 0x0;

        public const uint MQ_ERROR_SECURITY_DESCRIPTOR_TOO_SMALL = 0xC00E0023;

        //MQGetQueueSecurity
        //The MQGetQueueSecurity function retrieves the access control
        //security descriptor for the queue that you specify
        [DllImport("mqrt.dll", SetLastError=true)]
        public static extern uint MQGetQueueSecurity (
                  [MarshalAs(UnmanagedType.LPWStr)]
                  string lpwcsFormatName
                , int SecurityInformation
        , IntPtr pSecurityDescriptor
        , int nLength
        , out int lpnLengthNeeded
        );

        //MQSetQueueSecurity
        //The MQSetQueueSecurity function sets the access control
        //security descriptor for the queue that you specify.
        [DllImport("mqrt.dll", SetLastError=true, CharSet=CharSet.Auto)]
        public static extern uint MQSetQueueSecurity(
                  [MarshalAs(UnmanagedType.LPWStr)]
                  string lpwcsFormatName
                , int SecurityInformation
                , IntPtr pSecurityDescriptor
        );
    }

         public bool setQueueOwnerName(string formatName, string newOwner) {

            uint result;    //Return value of Win32 API call

            advapi32.SECURITY_DESCRIPTOR sd = new advapi32.SECURITY_DESCRIPTOR();

            IntPtr pSD = IntPtr.Zero;
            GCHandle hSD = GCHandle.Alloc(sd, GCHandleType.Pinned);
            pSD = hSD.AddrOfPinnedObject();

            //Call advapi32!InitializeSecurityDescriptor()
            //Call advapi32!SetSecurityDescriptorOwner()

            result = mqrt.MQSetQueueSecurity(
                  formatName
                , mqrt.OWNER_SECURITY_INFORMATION
                , pSD
            );

            //Free the Pinned Objects
            hSD.Free();

            return true;
        }
```
