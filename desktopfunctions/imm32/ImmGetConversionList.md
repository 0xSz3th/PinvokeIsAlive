
## C# Signature:
```cs
[DllImport("Imm32.dll", SetLastError=true)]
public static extern int ImmGetConversionList(
    IntPtr hKL,
    IntPtr hIMC,
    string lpSrc,
    IntPtr lpDst,
    int dwBufLen,
    int uFlag
    );
```

## VB Signature:
```cs
Declare Function ImmGetConversionList Lib "Imm32.dll" (TODO) As TODO
```

## Notes:
```cs
const int GCL_REVERSECONVERSION = 0x0002;
[StructLayout(LayoutKind.Sequential)]
public class CANDIDATELIST
{
    public int  dwSize;
    public int  dwStyle;
    public int  dwCount;
    public int  dwSelection;
    public int  dwPageStart;
    public int  dwPageSize;
    public int  dwOffset;
}
```

## Sample Code:
```cs
public string[] GetReverseConversion(IntPtr AHwnd,string AText)
{
    string[] strList = null;
    IntPtr hIMC = ImmGetContext(AHwnd);
    IntPtr hKL = GetKeyboardLayout(0);
    if ((hIMC != IntPtr.Zero)&&(hKL != IntPtr.Zero))
    {
        CANDIDATELIST list = new CANDIDATELIST();
        int dwSize = ImmGetConversionList(hKL,hIMC,AText,IntPtr.Zero,0,GCL_REVERSECONVERSION);
        if (dwSize>0)
        {
            IntPtr BufList = Marshal.AllocHGlobal(dwSize);
            ImmGetConversionList(hKL,hIMC,AText,BufList,dwSize,GCL_REVERSECONVERSION);
            Marshal.PtrToStructure(BufList,list);
            byte[] buf = new byte[dwSize];
            Marshal.Copy(BufList,buf,0,dwSize);
            Marshal.FreeHGlobal(BufList);
            int os = list.dwOffset;
            string str = System.Text.Encoding.Default.GetString(buf,os,buf.Length-os);
            str = Regex.Replace(str,@"\0+$","");
            char[] par = "\0".ToCharArray();
            strList = str.Split(par);
            ImmReleaseContext(this.Handle,hIMC);
        }
    }
    return strList;
}

private void button1_Click(object sender, System.EventArgs e)
{
    listBox1.Items.Clear();
    listBox1.Items.AddRange(GetReverseConversion(this.Handle,textBox1.Text));
}
```
