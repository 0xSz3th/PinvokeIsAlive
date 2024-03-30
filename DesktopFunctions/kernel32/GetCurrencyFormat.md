
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern int GetCurrencyFormat(uint Locale, uint dwFlags, string lpValue,
   [In, MarshalAs(UnmanagedType.LPStruct)]  lpFormat, IntPtr lpCurrencyStr, int cchCurrency);
```

## C# User-Defined Types
```cs
[StructLayout(LayoutKind.Sequential)]
    public class CURRENCYFMT
    {
        [MarshalAs(System.Runtime.InteropServices.UnmanagedType.U4)]
        public UInt32 uiNumDigits;
        [MarshalAs(System.Runtime.InteropServices.UnmanagedType.U4)]
        public UInt32 uiLeadingZero;
        [MarshalAs(System.Runtime.InteropServices.UnmanagedType.U4)]
        public UInt32 uiGrouping;
        [MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPWStr)]
        public String lpDecimalSep;
        [MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPWStr)]
        public String lpThousandSep;
        [MarshalAs(System.Runtime.InteropServices.UnmanagedType.U4)]
        public UInt32 uiNegativeOrder;
        [MarshalAs(System.Runtime.InteropServices.UnmanagedType.U4)]
        public UInt32 uiPositiveOrder;
        [MarshalAs(System.Runtime.InteropServices.UnmanagedType.LPWStr)]
        public String lpCurrencySymbol;
    };
```

## Notes:
```cs
0 => False - Don't show the leading zero.
    1 => True - Show the leading zero.
```

## Notes:
```cs
0 => $###.##
    1 => ###.##$
    2 => $ ###.##
    3 => ###.## $
```

## Notes:
```cs
0 => ($###.##)
     1 => -$###.##
     2 => $-###.##
     3 => $###.##-
     4 => (###.##$)
     5 => -###.##$
     6 => ###.##-$
     7 => ###.##$-
     8 => -###.## $
     9 => -$ ###.##
    10 => ###.## $-
    11 => $ ###.##-
    12 => $ -###.##
    13 => ###.##- $
    14 => ($ ###.##)
    15 => (###.## $)
```

## Sample Code:
```cs
/// <summary>
    /// Will convert a decimal to the specified currency format.
    /// </summary>
    /// <param name="numberToConvert">Must be a decimal number with no formatting.  If there is formatting
    /// on the number, it should be removed before calling this function.</param>
    /// <returns>Null if there is an error, otherwise the number formatted as currency.</returns>
    public string ConvertDecimalToCurrency(Decimal numberToConvert, CURRENCYFMT currencyFormat)
    {
        String sCurrency = null;
        long lRet = 0;

        //Find out the size of the converted string..
        lRet = GetCurrencyFormat(0, 0, numberToConvert.ToString(), currencyFormat, IntPtr.Zero, 0);

        if (0 != lRet)
        {
        //Get the formatted currency string

        IntPtr ptrCurrencyStr = Marshal.AllocHGlobal((int)lRet);

        lRet = GetCurrencyFormat(0, 0, numberToConvert.ToString(), currencyFormat, ptrCurrencyStr, (int)lRet);

        sCurrency = 0 == lRet ? null : Marshal.PtrToStringUni(ptrCurrencyStr);

        Marshal.FreeHGlobal(ptrCurrencyStr);
        }
        else
        {
        //Shouldn't be here, we should have received the size of the converted string.
        //See the error code that was returned.
        int error = Marshal.GetLastWin32Error();
        Trace.WriteLine("Error converting decimal to currency.  Error Number: " + error.ToString());
        }
```

## Sample Code:
```cs
return sCurrency;
    }

    private void cmdTest_Click(object sender, EventArgs e)
    {
        //Setup how the currency is going to be formatted.
        CURRENCYFMT currencyFormat = new CURRENCYFMT();
        currencyFormat.uiGrouping = Convert.ToUInt32(txtGrouping.Text);
        currencyFormat.uiLeadingZero = Convert.ToUInt32(cboLeadingZero.SelectedIndex);
        currencyFormat.lpCurrencySymbol = txtCurrencySymbol.Text;
        currencyFormat.lpDecimalSep = txtDecimalSep.Text;
        currencyFormat.lpThousandSep = txtThousandSep.Text;
        currencyFormat.uiNegativeOrder = Convert.ToUInt32(cboNegativeOrder.SelectedIndex);
        currencyFormat.uiNumDigits = Convert.ToUInt32(txtNumDigits.Text);
        currencyFormat.uiPositiveOrder = Convert.ToUInt32(cboPositiveOrder.SelectedIndex);

        txtConverted.Text = ConvertDecimalToCurrency(Convert.ToDecimal(txtConvert.Text), currencyFormat);
    }
```

## Alternative Managed API:
```cs
Decimal n = 100.53m;
  string sFormatted = n.ToString("C");
```
