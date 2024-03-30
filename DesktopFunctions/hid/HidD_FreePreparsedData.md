
## C# Signature:
```cs
[DllImport("hid.dll", SetLastError=true)]
static extern Boolean HidD_FreePreparsedData(IntPtr PreparsedData);
```

## VB Signature:
```cs
Declare Function HidD_FreePreparsedData Lib "hid.dll" (ByRef PreparsedData As Integer) As Boolean
```

## Sample Code:
```cs
internal HIDP_CAPS GetDeviceCapabilities( SafeFileHandle hidHandle ) 
    {         
        Byte[] preparsedDataBytes = new Byte[ 30 ]; 
        String preparsedDataString = null; 
        IntPtr preparsedDataPointer = new System.IntPtr(); 
        Int32 result = 0; 
        Boolean success = false; 
        Byte[] valueCaps = new Byte[ 1024 ]; // (the array size is a guess)

        try 
        {         

        success = HidD_GetPreparsedData( hidHandle, ref preparsedDataPointer );

        //  Copy the data at PreparsedDataPointer into a byte array.

        preparsedDataString = Convert.ToBase64String( preparsedDataBytes ); 

        result = HidP_GetCaps( preparsedDataPointer, ref Capabilities ); 
        if ( ( result != 0 ) ) 
        {             
            result = HidP_GetValueCaps(HidP_Input, ref valueCaps[0], ref Capabilities.NumberInputValueCaps, preparsedDataPointer); 

            success = HidD_FreePreparsedData( ref preparsedDataPointer );             
        }         
        } 
        catch ( Exception ex ) 
        { 
        DisplayException( MODULE_NAME, ex ); 
        throw ; 
        } 

        return Capabilities;         
    }
```
