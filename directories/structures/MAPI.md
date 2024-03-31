
## C# Structures:
```cs
/// <summary>
  /// A MapiFileDesc structure contains information about a file containing a message attachment 
  /// stored as a temporary file. 
  /// 
  /// The file can contain a static OLE object, an embedded OLE object, an embedded message, 
  /// and other types of files.
  /// </summary>
  [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
  public class MapiFileDesc {
    /// <summary>
    /// Reserved; must be zero.
    /// </summary>
    public uint ulReserved = 0;

    /// <summary>
    /// Bitmask of attachment flags. Flags are MAPI_OLE and MAPI_OLE_STATIC.
    /// 
    /// If neither flag is set, the attachment is treated as a data file. 
    /// </summary>
    public uint flFlags = 0;

    /// <summary>
    /// An integer used to indicate where in the message text to render the attachment.
    /// 
    /// Attachments replace the character found at a certain position in the message text. 
    /// That is, attachments replace the character in the MapiMessage structure field 
    /// lpszNoteText[nPosition]. A value of – 1 (0xFFFFFFFF) means the attachment position is 
    /// not indicated; the client application will have to provide a way for the user to 
    /// access the attachment. 
    /// </summary>
    public uint nPosition = 0xffffffff;

    /// <summary>
    /// Pointer to the fully qualified path of the attached file.
    /// 
    /// This path should include the disk drive letter and directory name.
    /// </summary>
    public string lpszPathName = string.Empty;

    /// <summary>
    /// Pointer to the attachment filename seen by the recipient, which may differ from the filename in
    /// the lpszPathName member if temporary files are being used. 
    /// 
    /// If the lpszFileName member is empty or NULL, the filename from lpszPathName is used. 
    /// </summary>
    public string lpszFileName = string.Empty;

    /// <summary>
    /// Pointer to the attachment file type, which can be represented with a MapiFileTagExt 
    /// structure.
    /// 
    /// A value of NULL indicates an unknown file type or a file type determined by the operating system. 
    /// </summary>
    public IntPtr lpFileType = IntPtr.Zero;
  }

  /// <summary>
  /// MapiFileTagExt structure specifies a message attachment's type at its creation 
  /// and its current form of encoding so that it can be restored to its original type at its destination.
  /// 
  /// A MapiFileTagExt structure defines the type of an attached file for purposes such as encoding and 
  /// decoding the file, choosing the correct application to launch when opening it, or any use that 
  /// requires full information regarding the file type. 
  /// 
  /// Client applications can use information in the lpTag and lpEncoding
  /// members of this structure to determine what to do with an attachment.
  /// </summary>
  [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
  public class MapiFileTagExt {
    /// <summary>
    /// Reserved; must be zero.
    /// </summary>
    public uint ulReserved = 0;

    /// <summary>
    /// The size, in bytes, of the value defined by the lpTag member.
    /// </summary>
    public uint cbTag = 0;

    /// <summary>
    /// Pointer to an X.400 object identifier indicating the type of the attachment in its original form, 
    /// for example "Microsoft Excel worksheet".
    /// </summary>
    public IntPtr lpTag = IntPtr.Zero;

    /// <summary>
    /// The size, in bytes, of the value defined by the lpEncoding member.
    /// </summary>
    public uint cbEncoding = 0;

    /// <summary>
    /// Pointer to an X.400 object identifier indicating the form in which the attachment is currently 
    /// encoded, for example MacBinary, UUENCODE, or binary.
    /// </summary>
    public IntPtr lpEncoding = IntPtr.Zero;
  }

  /// <summary>
  /// A MapiMessage structure contains information about a message.
  /// </summary>
  [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
  public class MapiMessage {
    /// <summary>
    /// Reserved; must be zero.
    /// </summary>
    public uint ulReserved = 0;

    /// <summary>
    /// Pointer to the text string describing the message subject, 
    /// typically limited to 256 characters or less.
    /// 
    /// If this member is empty or NULL, the user has not entered subject text.
    /// </summary>
    public string lpszSubject = string.Empty;

    /// <summary>
    /// Pointer to a string containing the message text.
    /// 
    /// If this member is empty or NULL, there is no message text.
    /// </summary>
    public string lpszNoteText = string.Empty;

    /// <summary>
    /// Pointer to a string indicating a non-IPM type of message.
    /// 
    /// Client applications can select message types for their non-IPM messages. 
    /// 
    /// Clients that only support IPM messages can ignore the lpszMessageType member 
    /// when reading messages and set it to empty or NULL when sending messages.
    /// </summary>
    public string lpszMessageType = null;

    /// <summary>
    /// Pointer to a string indicating the date when the message was received.
    /// 
    /// The format is YYYY/MM/DD HH:MM, using a 24-hour clock.
    /// </summary>
    public string lpszDateReceived = DateTime.Now.ToString("yyyy/MM/dd HH:mm");

    /// <summary>
    /// Pointer to a string identifying the conversation thread to which the message belongs. 
    /// 
    /// Some messaging systems can ignore and not return this member.
    /// </summary>
    public string lpszConversationID = string.Empty;

    /// <summary>
    /// Bitmask of message status flags. 
    /// 
    /// The flags are MAPI_RECEIPT_REQUESTED , MAPI_SENT, 
    /// and MAPI_UNREAD.
    /// </summary>
    public uint flFlags = 0;

    /// <summary>
    /// Pointer to a MapiRecipDesc structure containing information about the 
    /// sender of the message.
    /// </summary>
    public IntPtr lpOriginator = IntPtr.Zero;

    /// <summary>
    /// The number of message recipient structures in the array pointed to by the 
    /// lpRecips member. 
    /// 
    /// A value of zero indicates no recipients are included. 
    /// </summary>
    public uint nRecipCount = 0;

    /// <summary>
    /// Pointer to an array of MapiRecipDesc structures, each containing 
    /// information about a message recipient.
    /// </summary>
    public IntPtr lpRecips = IntPtr.Zero;

    /// <summary>
    /// The number of structures describing file attachments in the array pointed to by the 
    /// lpFiles member. 
    /// 
    /// A value of zero indicates no file attachments are included.
    /// </summary>
    public uint nFileCount = 0;

    /// <summary>
    /// Pointer to an array of MapiFileDesc structures, each containing 
    /// information about a file attachment.
    /// </summary>
    public IntPtr lpFiles = IntPtr.Zero;
  }

  /// <summary>
  /// A MapiRecipDesc structure contains information about a message sender or recipient.
  /// </summary>
  [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
  public class MapiRecipDesc {
    /// <summary>
    /// Reserved; must be zero.
    /// </summary>
    public uint ulReserved = 0;

    /// <summary>
    /// Contains a numeric value that indicates the type of recipient. 
    /// 
    /// Possible values are: 
    ///
    ///   Value  Constant   Meaning
    ///
    ///     0    MAPI_ORIG  Indicates the original sender of the message.
    ///     1    MAPI_TO    Indicates a primary message recipient.
    ///     2    MAPI_CC    Indicates a recipient of a message copy.
    ///     3    MAPI_BCC   Indicates a recipient of a blind copy.
    ///
    /// </summary>
    public uint ulRecipClass = MAPI_ORIG;

    /// <summary>
    /// Pointer to the display name of the message recipient or sender.
    /// </summary>
    public string lpszName = string.Empty;

    /// <summary>
    /// Optional pointer to the recipient or sender's address; this address is provider-specific message 
    /// delivery data. Generally, the messaging system provides such addresses for inbound messages. 
    /// 
    /// For outbound messages, the lpszAddress member can point to an address entered by the user for 
    /// a recipient not in an address book (that is, a custom recipient). 
    /// 
    /// The format of an address pointed to by the lpszAddress member is [address type][e-mail address].
    /// Examples of valid addresses are FAX:206-555-1212 and SMTP:M@X.COM. 
    /// </summary>
    public string lpszAddress = string.Empty;

    /// <summary>
    /// The size, in bytes, of the entry identifier pointed to by the lpEntryID member.
    /// </summary>
    public uint ulEIDSize = 0;

    /// <summary>
    /// Pointer to an opaque entry identifier used by a messaging system service provider to identify the 
    /// message recipient. Entry identifiers have meaning only for the service provider; 
    /// client applications will not be able to decipher them. The messaging system uses this member 
    /// to return valid entry identifiers for all recipients or senders listed in the address book.
    /// </summary>
    public IntPtr lpEntryID = IntPtr.Zero;
  }
```

## VB Structures:
```cs
''' <summary>
    ''' A MapiMessage structure contains information about a message.
    ''' </summary>
    <StructLayout(LayoutKind.Sequential)> _
    Public Structure MapiMessage

    ''' <summary>
    ''' Reserved; must be zero.
    ''' </summary>
    Public ulReserved As UInt32

    ''' <summary>
    ''' Pointer to the text string describing the message subject, 
    ''' typically limited to 256 characters or less.
    ''' 
    ''' If this member is empty or NULL, the user has not entered subject text.
    ''' </summary>
    Public lpszSubject As String

    ''' <summary>
    ''' Pointer to a string containing the message text.
    ''' 
    ''' If this member is empty or NULL, there is no message text.
    ''' </summary>
    Public lpszNoteText As String

    ''' <summary>
    ''' Pointer to a string indicating a non-IPM type of message.
    ''' 
    ''' Client applications can select message types for their non-IPM messages. 
    ''' 
    ''' Clients that only support IPM messages can ignore the lpszMessageType member 
    ''' when reading messages and set it to empty or NULL when sending messages.
    ''' </summary>
    Public lpszMessageType As String

    ''' <summary>
    ''' Pointer to a string indicating the date when the message was received.
    ''' 
    ''' The format is YYYY/MM/DD HH:MM, using a 24-hour clock.
    ''' </summary>
    Public lpszDateReceived As String

    ''' <summary>
    ''' Pointer to a string identifying the conversation thread to which the message belongs. 
    ''' 
    ''' Some messaging systems can ignore and not return this member.
    ''' </summary>
    Public lpszConversationID As String

    ''' <summary>
    ''' Bitmask of message status flags. 
    ''' 
    ''' The flags are MAPI_RECEIPT_REQUESTED , MAPI_SENT, 
    ''' and MAPI_UNREAD.
    ''' </summary>
    Public flFlags As UInt32

    ''' <summary>
    ''' Pointer to a MapiRecipDesc structure containing information about the 
    ''' sender of the message.
    ''' </summary>
    Public lpOriginator As IntPtr

    ''' <summary>
    ''' The number of message recipient structures in the array pointed to by the 
    ''' lpRecips member. 
    ''' 
    ''' A value of zero indicates no recipients are included. 
    ''' </summary>
    Public nRecipCount As UInt32

    ''' <summary>
    ''' Pointer to an array of MapiRecipDesc structures, each containing 
    ''' information about a message recipient.
    ''' </summary>
    Public lpRecips As IntPtr

    ''' <summary>
    ''' The number of structures describing file attachments in the array pointed to by the 
    ''' lpFiles member. 
    ''' 
    ''' A value of zero indicates no file attachments are included.
    ''' </summary>
    Public nFileCount As UInt32

    ''' <summary>
    ''' Pointer to an array of MapiFileDesc structures, each containing 
    ''' information about a file attachment.
    ''' </summary>
    Public lpFiles As IntPtr

    End Structure

    ''' <summary>
    ''' A MapiFileDesc structure contains information about a file containing a message attachment 
    ''' stored as a temporary file. 
    ''' 
    ''' The file can contain a static OLE object, an embedded OLE object, an embedded message, 
    ''' and other types of files.
    ''' </summary>
    <StructLayout(LayoutKind.Sequential)> _
    Public Structure MapiFileDesc

    ''' <summary>
    ''' Reserved; must be zero.
    ''' </summary>
    Public ulReserved As UInt32

    ''' <summary>
    ''' Bitmask of attachment flags. Flags are MAPI_OLE and MAPI_OLE_STATIC.
    ''' 
    ''' If neither flag is set, the attachment is treated as a data file. 
    ''' </summary>
    Public flFlags As UInt32

    ''' <summary>
    ''' An integer used to indicate where in the message text to render the attachment.
    ''' 
    ''' Attachments replace the character found at a certain position in the message text. 
    ''' That is, attachments replace the character in the MapiMessage structure field 
    ''' lpszNoteText[nPosition> _. A value of – 1 (0xFFFFFFFF) means the attachment position is 
    ''' not indicated; the client application will have to provide a way for the user to 
    ''' access the attachment. 
    ''' </summary>
    Public nPosition As UInt32

    ''' <summary>
    ''' Pointer to the fully qualified path of the attached file.
    ''' 
    ''' This path should include the disk drive letter and directory name.
    ''' </summary>
    Public lpszPathName As String

    ''' <summary>
    ''' Pointer to the attachment filename seen by the recipient, which may differ from the filename in
    ''' the lpszPathName member if temporary files are being used. 
    ''' 
    ''' If the lpszFileName member is empty or NULL, the filename from lpszPathName is used. 
    ''' </summary>
    Public lpszFileName As String

    ''' <summary>
    ''' Pointer to the attachment file type, which can be represented with a MapiFileTagExt 
    ''' structure.
    ''' 
    ''' A value of NULL indicates an unknown file type or a file type determined by the operating system. 
    ''' </summary>
    Public lpFileType As IntPtr

    End Structure

    ''' <summary>
    ''' MapiFileTagExt structure specifies a message attachment's type at its creation 
    ''' and its current form of encoding so that it can be restored to its original type at its destination.
    ''' 
    ''' A MapiFileTagExt structure defines the type of an attached file for purposes such as encoding and 
    ''' decoding the file, choosing the correct application to launch when opening it, or any use that 
    ''' requires full information regarding the file type. 
    ''' 
    ''' Client applications can use information in the lpTag and lpEncoding
    ''' members of this structure to determine what to do with an attachment.
    ''' </summary>
    <StructLayout(LayoutKind.Sequential)> _
    Public Structure MapiFileTagExt

    ''' <summary>
    ''' Reserved; must be zero.
    ''' </summary>
    Public ulReserved As UInt32

    ''' <summary>
    ''' The size, in bytes, of the value defined by the lpTag member.
    ''' </summary>
    Public cbTag As UInt32

    ''' <summary>
    ''' Pointer to an X.400 object identifier indicating the type of the attachment in its original form, 
    ''' for example "Microsoft Excel worksheet".
    ''' </summary>
    Public lpTag As IntPtr

    ''' <summary>
    ''' The size, in bytes, of the value defined by the lpEncoding member.
    ''' </summary>
    Public cbEncoding As UInt32

    ''' <summary>
    ''' Pointer to an X.400 object identifier indicating the form in which the attachment is currently 
    ''' encoded, for example MacBinary, UUENCODE, or binary.
    ''' </summary>
    Public lpEncoding As IntPtr

    End Structure

    ''' <summary>
    ''' A MapiRecipDesc structure contains information about a message sender or recipient.
    ''' </summary>
    <StructLayout(LayoutKind.Sequential)> _
    Public Structure MapiRecipDesc

    ''' <summary>
    ''' Reserved; must be zero.
    ''' </summary>
    Public ulReserved As UInt32

    ''' <summary>
    ''' Contains a numeric value that indicates the type of recipient. 
    ''' 
    ''' Possible values are: 
    '''
    '''   Value  Constant   Meaning
    '''
    '''     0    MAPI_ORIG  Indicates the original sender of the message.
    '''     1    MAPI_TO    Indicates a primary message recipient.
    '''     2    MAPI_CC    Indicates a recipient of a message copy.
    '''     3    MAPI_BCC   Indicates a recipient of a blind copy.
    '''
    ''' </summary>
    Public ulRecipClass As UInt32

    ''' <summary>
    ''' Pointer to the display name of the message recipient or sender.
    ''' </summary>
    Public lpszName As String

    ''' <summary>
    ''' Optional pointer to the recipient or sender's address; this address is provider-specific message 
    ''' delivery data. Generally, the messaging system provides such addresses for inbound messages. 
    ''' 
    ''' For outbound messages, the lpszAddress member can point to an address entered by the user for 
    ''' a recipient not in an address book (that is, a custom recipient). 
    ''' 
    ''' The format of an address pointed to by the lpszAddress member is [address type> _[e-mail address> _.
    ''' Examples of valid addresses are FAX:206-555-1212 and SMTP:M@X.COM. 
    ''' </summary>
    Public lpszAddress As String

    ''' <summary>
    ''' The size, in bytes, of the entry identifier pointed to by the lpEntryID member.
    ''' </summary>
    Public ulEIDSize As UInt32

    ''' <summary>
    ''' Pointer to an opaque entry identifier used by a messaging system service provider to identify the 
    ''' message recipient. Entry identifiers have meaning only for the service provider; 
    ''' client applications will not be able to decipher them. The messaging system uses this member 
    ''' to return valid entry identifiers for all recipients or senders listed in the address book.
    ''' </summary>
    Public lpEntryID As IntPtr

    End Structure
```
