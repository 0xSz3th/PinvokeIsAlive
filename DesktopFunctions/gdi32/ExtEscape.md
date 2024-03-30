
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern int ExtEscape(IntPtr hdc, int nEscape, int cbInput,
   string lpszInData, int cbOutput, IntPtr lpszOutData);
```

## VB.NET Signature:
```cs
<DllImport("gdi32.dll")> _
    Public Shared Function ExtEscape(ByVal hdc As IntPtr, ByVal nEscape As Integer, ByVal cbInput As Integer, ByVal lpszInData As String, ByVal cbOutput As Integer, ByRef lpszOutData As IntPtr) As Integer
    End Function
```

## Sample Code:
```cs
//By Justin Alexander, aka TheLoneCabbage

        static Int32 GETTECHNOLOGY = 20;
        static Int32 QUERYESCSUPPORT = 8;
        static Int32 POSTSCRIPT_PASSTHROUGH     =     4115;
        static Int32 ENCAPSULATED_POSTSCRIPT= 4116;

        static Int32 POSTSCRIPT_IDENTIFY    =     4117;
        static Int32 POSTSCRIPT_INJECTION       =     4118;
        static Int32 POSTSCRIPT_DATA        =     37;
        static Int32 POSTSCRIPT_IGNORE      =     38;

        static bool PrinterSupportsPostScript(string printername)
        {
            ArrayList PSChecks=new ArrayList();
            PSChecks.Add(POSTSCRIPT_PASSTHROUGH);
            PSChecks.Add(ENCAPSULATED_POSTSCRIPT);
            PSChecks.Add(POSTSCRIPT_IDENTIFY);
            PSChecks.Add(POSTSCRIPT_INJECTION);
            PSChecks.Add(POSTSCRIPT_DATA);
            PSChecks.Add(POSTSCRIPT_IGNORE);

            IntPtr hDC=IntPtr.Zero;;
            IntPtr BLOB=IntPtr.Zero;

            try
            {
                hDC =CreateDC(null,printername,0,IntPtr.Zero);

                int isz=4;
                BLOB = Marshal.AllocCoTaskMem(isz);
                Marshal.WriteInt32(BLOB,GETTECHNOLOGY);

                int test=ExtEscape( hDC, QUERYESCSUPPORT, 4, BLOB, 0, IntPtr.Zero);
                if(test==0) return false; // printer driver does not support GETTECHNOLOGY Checks.

                foreach(Int32 val in PSChecks)
                {
                    Marshal.WriteInt32(BLOB,val);
                    test = ExtEscape(hDC,QUERYESCSUPPORT,isz,BLOB,0, IntPtr.Zero);
                    if(test!=0) return true; // if any of the checks pass, return true
                }
            }
            catch(Exception ex){Trace.WriteLine(ex);}
            finally
            {
                if(hDC!=IntPtr.Zero) DeleteDC(hDC);

                if(BLOB!=IntPtr.Zero) Marshal.Release(BLOB);
            };

            return false;

        }
```
