
## C# Signature:
```cs
/// <summary>
  /// The MAPISendMail function sends a message.
  /// 
  /// This function differs from the MAPISendDocuments function in that it allows greater 
  /// flexibility in message generation.
  /// </summary>
  [DllImport("MAPI32.DLL", CharSet=CharSet.Ansi)]
  public static extern uint MAPISendMail(IntPtr lhSession, IntPtr ulUIParam, 
    MapiMessage lpMessage, uint flFlags, uint ulReserved);
```

## VB Signature:
```cs
<DllImport("MAPI32.DLL")> _
    Private Shared Function MAPISendMail(ByVal sess As IntPtr, ByVal hwnd As IntPtr, ByVal message As MapiMessage, 
       ByVal flg As Integer, ByVal rsv As Integer) As Integer
    End Function
```

## Sample Code:
```cs
[DllImport("MAPI32.DLL")]
    static extern int MAPISendMail(IntPtr sess, IntPtr hwnd, MapiMessage message, int flg, int rsv);

    public int SendMail(string fileName)
    {
        MapiMessage msg = new MapiMessage();
        msg.subject = "Hello World!";
        msg.noteText = "See attached file for details";
        msg.files = GetAttachments(fileName, out msg.fileCount);

        int result = MAPISendMail(new IntPtr(0), new IntPtr(0), msg, 0x00000001 | 0x00000008, 0);
        if (result > 1 || result < 0)
        throw new System.InvalidOperationException();
        return result;
    }

    IntPtr GetAttachments(string fileName, out int fileCount)
    {
        int size = Marshal.SizeOf(typeof(MapiFileDesc));
        IntPtr intPtr = Marshal.AllocHGlobal(size);

        MapiFileDesc mapiFileDesc = new MapiFileDesc();
        //An integer used to indicate where in the message text to render the attachment. 
        mapiFileDesc.position = -1;
        int ptr = (int)intPtr;

        mapiFileDesc.name = Path.GetFileName(fileName);
        mapiFileDesc.path = fileName;
        Marshal.StructureToPtr(mapiFileDesc, (IntPtr)ptr, false);
        ptr += size;

        fileCount = 1;
        return intPtr;
    }
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
    public class MapiMessage
    {
    public int reserved;
    public string subject;
    public string noteText;
    public string messageType;
    public string dateReceived;
    public string conversationID;
    public int flags;
    public IntPtr originator;
    public int recipCount;
    public IntPtr recips;
    public int fileCount;
    public IntPtr files;
    }

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
    public class MapiFileDesc
    {
    public int reserved;
    public int flags;
    public int position;
    public string path;
    public string name;
    public IntPtr type;
    }
```
