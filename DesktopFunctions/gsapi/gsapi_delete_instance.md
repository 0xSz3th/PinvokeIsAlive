
## C# Signature:
```cs
[DllImport("gsdll32.dll", CharSet = CharSet.Ansi, CallingConvention = CallingConvention.StdCall)]
    private static extern void gsapi_delete_instance(System.IntPtr pinstance);
```

## VB Signature:
```cs
<DllImport("gsdll32.dll", CharSet:= CharSet.Ansi, CallingConvention:= CallingConvention.StdCall)> _
    Private Shared Sub gsapi_delete_instance(ByVal pinstance As System.IntPtr)
    End Sub
```

## Sample Code:
```cs
/* Assume pinstance has been initialized using gsapi_new_instance. */
   System.IntPtr pinstance;  /* Class instance variable */

    private void button1_Click(object sender, EventArgs e)
    {
    if (pinstance != System.IntPtr.Zero)
    {
       int ret = gsapi_exit(pinstance);
       gsapi_delete_instance(pinstance);
       pinstance = System.IntPtr.Zero;
     }

    }
```
