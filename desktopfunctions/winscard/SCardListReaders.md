
## C# Signature:
```cs
[DllImport("winscard.dll", EntryPoint="SCardListReadersA", CharSet=CharSet.Ansi)]
    public static extern int SCardListReaders(
      int hContext, 
      byte[] mszGroups,
      byte[] mszReaders,
      ref UInt32 pcchReaders
      );
```

## VB.NET Signature:
```cs
<DllImport("WinScard.dll", EntryPoint:="SCardListReadersA", CharSet:=CharSet.Ansi)>
    Public Shared Function SCardListReaders(
      hContext As IntPtr,
      mszGroups As Byte(),
      mszReaders As Byte(),
      ByRef pcchReaders As UInt32
      ) As Integer
    End Function
```

## Sample Code:
```cs
long ret = 0;
int hContext;
Int32 pcchReaders = 0;
int nullindex = -1;
char nullchar = (char) 0;
ArrayList readersList = new ArrayList();

//establish context
ret = SCardEstablishContext(SCARD_SCOPE_USER,IntPtr.Zero,IntPtr.Zero,out hContext);

//get readers buffer len
ret = SCardListReaders(hContext,IntPtr.Zero,null,ref pcchReaders);
byte[] mszReaders = new byte[pcchReaders];

// fill readers' buffer
ret = SCardListReaders(hContext,IntPtr.Zero ,mszReaders, ref pcchReaders);

//fill readersList
//remember that readers is a multistring with a double trailing \0
// This is much easier and faster to do the allocation like this than the looping way
//ASCIIEncoding asc = new ASCIIEncoding();
//String[] Readers = asc.GetString( mszReaders ).Split( '\0' );
ASCIIEncoding ascii = new ASCIIEncoding();
string currbuff = ascii.GetString(mszReaders);
int len = pcchReaders;

while (currbuff[0]!=nullchar)
{
  nullindex = currbuff.IndexOf(nullchar);   //get null end character
  string reader = currbuff.Substring(0, nullindex);
  readersList.Add(reader);
  len = len-(reader.Length+1);
  currbuff = currbuff.Substring(nullindex+1,len);            
}

ret = SCardReleaseContext(hContext);
```
