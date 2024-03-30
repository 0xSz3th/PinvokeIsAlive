
## C# Signature:
```cs
[DllImport("winscard.dll", SetLastError=true)]
static extern Int32 SCardGetAttrib(
   IntPtr hCard,            // Reference value returned from SCardConnect
   UInt32 dwAttrId,         // Identifier for the attribute to get
   byte[] pbAttr,           // Pointer to a buffer that receives the attribute
   ref IntPtr pcbAttrLen    // Length of pbAttr in bytes
);
```

## VB Signature:
```cs
Declare Function SCardGetAttrib Lib "winscard.dll" (TODO) As TODO
```

## Sample Code:
```cs
// SCARD_ATTR_ATR_STRING = SCARD_ATTR_VALUE(SCARD_CLASS_ICC_STATE, 0x0303) in WinSCard.h
  const UInt32 SCARD_ATTR_ATR_STRING = 0x00090303;    
  IntPtr hCard;    // Handle to the card
  Int32 ret;

  // Copy code to establish context here

  // Copy code to connect to the card here

  // Get the Answer to Rest
  byte[] pbAttr = new byte[255];
  IntPtr pcbAttrLen = new IntPtr(pbAttr.Length);
  ret = SCardGetAttrib(hCard, SCARD_ATTR_ATR_STRING, pbAttr, ref pcbAttrLen);
```
