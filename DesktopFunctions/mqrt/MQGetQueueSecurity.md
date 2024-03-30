
## C# Signature:
```cs
[DllImport("mqrt.dll", CharSet = CharSet.Unicode)]
public static extern uint MQGetQueueSecurity (
      [MarshalAs(UnmanagedType.LPWStr)]
      string lpwcsFormatName
    , int SecurityInformation
    , IntPtr pSecurityDescriptor
    , int nLength
    , ref int lpnLengthNeeded
);
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
        [DllImport("mqrt.dll", CharSet = CharSet.Unicode)]
        public static extern uint MQGetQueueSecurity (
                  [MarshalAs(UnmanagedType.LPWStr)]
                  string lpwcsFormatName
                , int SecurityInformation
                , IntPtr pSecurityDescriptor
                , int nLength
                , ref int lpnLengthNeeded
        );

    }
```

## Sample Code:
```cs
private bool getQueueOwnerNameFromMSMQ(string formatName, ref string owner) {
            byte[] securityDescriptor;
            int length;
            int lengthNeeded;
            uint result;

            //Call MQGetQueueSecurity two times. The first time, set the nLength
            //parameter to 0. The function then informs you of the size that you need for the
            //security descriptor in lpnLengthNeeded.
            result = mqrt.MQGetQueueSecurity(
                      formatName
                    , mqrt.OWNER_SECURITY_INFORMATION
                    , IntPtr.Zero
                    , 0
                    , ref lengthNeeded);

            if (mqrt.MQ_ERROR_SECURITY_DESCRIPTOR_TOO_SMALL == result) {
                //This is expected. Continue.
            } else {
                //Something else went wrong. Display error, and then exit.
                string message = "There was an error calling MQGetQueueSecurity." 
                    + Environment.NewLine
                    + "Error Number:  " + result.ToString();
                string caption = "MQGetQueueSecurity Error";
                this.showError(message, caption);
                return false;
            }

            //Now we know how big to make the security descriptor.
            length = lengthNeeded;
            securityDescriptor = new byte[length];

            //Get a pointer to the SD
            IntPtr lpSD = new IntPtr();
            GCHandle hSD = GCHandle.Alloc(securityDescriptor, GCHandleType.Pinned);
            lpSD = hSD.AddrOfPinnedObject();

            //Call MQGetQueueSecurity
            result = mqrt.MQGetQueueSecurity(
                      formatName
                    , mqrt.OWNER_SECURITY_INFORMATION
                    , lpSD
                    , length
                    , ref lengthNeeded);

            if (mqrt.MQ_OK != result) {
                //Something else went wrong. Display error, and then exit.
                string message = "There was an error calling MQGetQueueSecurity to read the SecurityDescriptor." 
                    + Environment.NewLine
                    + "Error Number:  " + result.ToString();
                string caption = "MQGetQueueSecurity Error";
                this.showError(message, caption);
                return false;
            }

            hSD.Free();

            //Function call to break out the owner name from the SD
            //Left out as an exercise
            //owner = getSecurityDescriptorOwnerName(securityDescriptor);

            return true;
        }
```
