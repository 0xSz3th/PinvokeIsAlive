
## C# Constants:
```cs
/// <summary>
  /// A null session handle.
  /// </summary>
  public readonly IntPtr lhSessionNull = IntPtr.Zero;

  /// <summary>
  /// Indicates the original sender of the message.
  /// </summary>
  public const uint MAPI_ORIG = 0;

  /// <summary>
  /// Indicates a primary message recipient.
  /// </summary>
  public const uint MAPI_TO = 1;

  /// <summary>
  /// Indicates a recipient of a message copy.
  /// </summary>
  public const uint MAPI_CC = 2; 

  /// <summary>
  /// Indicates a recipient of a blind copy.
  /// </summary>
  public const uint MAPI_BCC = 3;

  /// <summary>
  /// The message has not been read.
  /// </summary>
  public const uint MAPI_UNREAD = 0x00000001;

  /// <summary>
  /// A receipt notification is requested. 
  /// 
  /// Client applications set this flag when sending a message.
  /// </summary>
  public const uint MAPI_RECEIPT_REQUESTED = 0x00000002;

  /// <summary>
  /// The message has been sent.
  /// </summary>
  public const uint MAPI_SENT = 0x00000004;

  /// <summary>
  /// A logon dialog box should be displayed to prompt the user for logon information. 
  /// 
  /// If the user needs to provide a password and profile name to enable a successful logon, 
  /// MAPI_LOGON_UI must be set. 
  /// </summary>
  public const uint MAPI_LOGON_UI = 0x00000001;

  /// <summary>
  /// MAPILogon should only prompt for a password and not allow the user to change the profile name. 
  ///
  /// Either MAPI_PASSWORD_UI or MAPI_LOGON_UI should not be set, since the intent is 
  /// to select between two different dialog boxes for logon.
  /// </summary>
  public const uint MAPI_PASSWORD_UI = 0x00020000;

  /// <summary>
  /// An attempt should be made to create a new session rather than acquire the environment's shared session. 
  ///
  /// If the MAPI_NEW_SESSION flag is not set, MAPILogon uses an existing shared session.
  /// </summary>
  public const uint MAPI_NEW_SESSION = 0x00000002;

  /// <summary>
  /// An attempt should be made to download all of the user's messages before returning. I
  /// 
  /// If the MAPI_FORCE_DOWNLOAD flag is not set, messages can be downloaded in the background 
  /// after the function call returns.
  /// </summary>
  public const uint MAPI_FORCE_DOWNLOAD = 0x00001000;

  /// <summary>
  /// Log on with extended capabilities. 
  /// 
  /// This flag indicates an Extended MAPI session will be created.
  /// </summary>
  public const uint MAPI_EXTENDED = 0x00000020;

  /// <summary>
  /// MAPI should not inform the MAPI spooler of the session's existence. The result is that no messages can be sent or received within 
  ///   the session   except through a tightly coupled store and transport pair. A calling client sets this flag if it is acting as an agent, if 
  ///   configuration work must be done, or if the client is browsing the available message stores.
  /// </summary>
  public const uint MAPI_NO_MAIL = 0x00008000;

  /// <summary>
  /// A dialog box should be displayed to prompt the user for recipients and other sending options. 
  /// 
  /// When MAPI_DIALOG is not set, at least one recipient must be specified.
  /// </summary>
  public const uint MAPI_DIALOG = 0x00000008;

  /// <summary>
  /// Only unread messages of the specified type should be enumerated. 
  /// 
  /// If this flag is not set, MAPIFindNext can return any message of the specified type. 
  /// </summary>
  public const uint MAPI_UNREAD_ONLY = 0x00000020;

  /// <summary>
  /// The attachment is an OLE object.
  /// If MAPI_OLE_STATIC is also set, the attachment is a static OLE object. 
  /// If MAPI_OLE_STATIC is not set, the attachment is an embedded OLE object. 
  /// </summary>
  public const uint MAPI_OLE = 0x00000001;

  /// <summary>
  /// The attachment is a static OLE object.
  /// </summary>
  public const uint MAPI_OLE_STATIC = 0x00000002;

  /// <summary>
  /// The message identifiers returned should be in the order of time received. 
  /// MAPIFindNext calls can take longer if this flag is set.
  /// Some implementations cannot honor this request and return the MAPI_E_NOT_SUPPORTED value.
  /// </summary>
  public const uint MAPI_GUARANTEE_FIFO = 0x00000100;

  /// <summary>
  /// The returned message identifier can be as long as 512 characters. 
  /// 
  /// If this flag is set, the lpszMessageID parameter must be large enough to accomodate 512 characters. 
  /// 
  /// Older versions of MAPI supported smaller message identifiers (64 bytes) and did not include this flag.
  /// MAPIFindNext will succeed without this flag set as long as lpszMessageID is large enough 
  /// to hold the message identifier. If lpszMessageID cannot hold the message identifier, 
  /// MAPIFindNext will fail. 
  /// </summary>
  public const uint MAPI_LONG_MSGID = 0x00004000;

  /// <summary>
  /// MAPIReadMail does not mark the message as read. 
  /// 
  /// Marking a message as read affects its appearance in the user interface and generates a read receipt. 
  /// 
  /// If the messaging system does not support this flag, MAPIReadMail always marks the
  /// message as read. If MAPIReadMail encounters an error, it leaves the message unread. 
  /// </summary>
  public const uint MAPI_PEEK = 0x00000080;

  /// <summary>
  /// MAPIReadMail should not copy file attachments but should write message text into the 
  /// MapiMessage structure. 
  /// 
  /// MAPIReadMail ignores this flag if the calling application has set the 
  /// MAPI_ENVELOPE_ONLY flag. Setting the MAPI_SUPPRESS_ATTACH flag enhances performance.
  /// </summary>
  public const uint MAPI_SUPPRESS_ATTACH = 0x00000800;

  /// <summary>
  /// MAPIReadMail should read the message header only. 
  /// 
  /// File attachments are not copied to temporary files, and neither temporary file names nor message 
  /// text is written. Setting this flag enhances performance.
  /// </summary>
  public const uint MAPI_ENVELOPE_ONLY = 0x00000040;

  /// <summary>
  /// MAPIReadMail should write the message text to a temporary file 
  /// and add it as the first attachment in the attachment list.
  /// </summary>
  public const uint MAPI_BODY_AS_FILE = 0x00000200;

  /// <summary>
  /// The caller is requesting that the dialog box be read-only, prohibiting changes.
  /// 
  /// MAPIDetails might or might not honor the request. 
  /// </summary>
  public const uint MAPI_AB_NOMODIFY = 0x00000400;

  /// <summary>
  /// The call succeeded.
  /// </summary>
  public const uint MAPI_SUCCESS_SUCCESS = 0;

  /// <summary>
  /// The user canceled one of the dialog boxes.
  /// </summary>
  public const uint MAPI_USER_ABORT = 1;

  /// <summary>
  /// The user canceled one of the dialog boxes.
  /// </summary>
  public const uint MAPI_E_USER_ABORT = MAPI_USER_ABORT;

  /// <summary>
  /// One or more unspecified errors occurred.
  /// </summary>
  public const uint MAPI_E_FAILURE = 2;

  /// <summary>
  /// There was no default logon, and the user failed to log on successfully when the logon dialog box 
  /// was displayed.
  /// </summary>
  public const uint MAPI_E_LOGON_FAILURE = 3;

  /// <summary>
  /// There was no default logon, and the user failed to log on successfully when the logon dialog box 
  /// was displayed.
  /// </summary>
  public const uint MAPI_E_LOGIN_FAILURE = MAPI_E_LOGON_FAILURE;

  /// <summary>
  /// A file could not be written because there was not enough space on the disk. 
  /// </summary>
  public const uint MAPI_E_DISK_FULL = 4;

  /// <summary>
  /// There was insufficient memory to proceed.
  /// </summary>
  public const uint MAPI_E_INSUFFICIENT_MEMORY = 5;

  /// <summary>
  /// Access to the MAPI client was denied.
  /// </summary>
  public const uint MAPI_E_ACCESS_DENIED = 6;

  /// <summary>
  /// The user had too many sessions open simultaneously.
  /// </summary>
  public const uint MAPI_E_TOO_MANY_SESSIONS = 8;

  /// <summary>
  /// There were too many file attachments.
  /// </summary>
  public const uint MAPI_E_TOO_MANY_FILES = 9;

  /// <summary>
  /// There were too many recipients.
  /// </summary>
  public const uint MAPI_E_TOO_MANY_RECIPIENTS = 10;

  /// <summary>
  /// The specified attachment was not found.
  /// </summary>
  public const uint MAPI_E_ATTACHMENT_NOT_FOUND = 11;

  /// <summary>
  /// The specified attachment could not be opened.
  /// </summary>
  public const uint MAPI_E_ATTACHMENT_OPEN_FAILURE = 12;

  /// <summary>
  /// An attachment could not be written to a temporary file.
  /// </summary>
  public const uint MAPI_E_ATTACHMENT_WRITE_FAILURE = 13;

  /// <summary>
  /// A recipient did not appear in the address list.
  /// </summary>
  public const uint MAPI_E_UNKNOWN_RECIPIENT = 14;

  /// <summary>
  /// The type of a recipient was not MAPI_TO, MAPI_CC, or MAPI_BCC.
  /// </summary>
  public const uint MAPI_E_BAD_RECIPTYPE = 15;

  /// <summary>
  /// A matching message could not be found.
  /// </summary>
  public const uint MAPI_E_NO_MESSAGES = 16;

  /// <summary>
  /// An invalid message identifier was passed.
  /// </summary>
  public const uint MAPI_E_INVALID_MESSAGE = 17;

  /// <summary>
  /// The text in the message was too large.
  /// </summary>
  public const uint MAPI_E_TEXT_TOO_LARGE = 18;

  /// <summary>
  /// An invalid session handle was used.
  /// </summary>
  public const uint MAPI_E_INVALID_SESSION = 19;

  /// <summary>
  /// An unsupported type was passed.
  /// </summary>
  public const uint MAPI_E_TYPE_NOT_SUPPORTED = 20;

  /// <summary>
  /// A recipient matched more than one of the recipient descriptor structures.
  /// </summary>
  public const uint MAPI_E_AMBIGUOUS_RECIPIENT = 21;

  /// <summary>
  /// A recipient matched more than one of the recipient descriptor structures.
  /// </summary>
  public const uint MAPI_E_AMBIG_RECIP = MAPI_E_AMBIGUOUS_RECIPIENT;

  /// <summary>
  /// The specified message was in use by another session or process.
  /// </summary>
  public const uint MAPI_E_MESSAGE_IN_USE = 22;

  /// <summary>
  /// A non-specific networking failure occurred.
  /// </summary>
  public const uint MAPI_E_NETWORK_FAILURE = 23;

  /// <summary>
  /// The value of the nEditFields parameter was outside the range of 0 through 4.
  /// </summary>
  public const uint MAPI_E_INVALID_EDITFIELDS = 24;

  /// <summary>
  /// One or more recipients were invalid or did not resolve to any address.
  /// </summary>
  public const uint MAPI_E_INVALID_RECIPS = 25;

  /// <summary>
  /// The operation was not supported by the underlying messaging system.
  /// </summary>
  public const uint MAPI_E_NOT_SUPPORTED = 26;
```

## VB Constants:
```cs
VB CONSTANTS ' Added by Dewayne Gunter
```

## Notes: It is fairly easy to edit between c# and vb cSharp declares type first then name
```cs
Public Const MAPI_ORIG As UInteger = 0
    Public Const MAPI_TO As UInteger = 1
    Public Const MAPI_CC As UInteger = 2
    Public Const MAPI_BCC As UInteger = 3
    Public Const MAPI_UNREAD As UInteger = &H1
    Public Const MAPI_RECEIPT_REQUESTED As UInteger = &H2
    Public Const MAPI_SENT As UInteger = &H4
    Public Const MAPI_LOGON_UUI As UInteger = &H1
    Public Const MAPI_PASSWORD_UUI As UInteger = &H20000
    Public Const MAPI_NEW_SESSION As UInteger = &H2
    Public Const MAPI_FORCE_DOWNLOAD As UInteger = &H1000
    Public Const MAPI_EXTENDED As UInteger = &H20
    Public Const MAPI_NO_MAIL As UInteger = &H8000
    Public Const MAPI_DIALOG As UInteger = &H8
    Public Const MAPI_UNREAD_ONLY As UInteger = &H20
    Public Const MAPI_OLE As UInteger = &H1
    Public Const MAPI_OLE_STATIC As UInteger = &H2
    Public Const MAPI_GUARANTEE_FIFO As UInteger = &H100
    Public Const MAPI_LONG_MSGID As UInteger = &H4000
    Public Const MAPI_PEEK As UInteger = &H80
    Public Const MAPI_SUPPRESS_ATTACH As UInteger = &H800
    Public Const MAPI_ENVELOPE_ONLY As UInteger = &H40
    Public Const MAPI_BODY_AS_FILE As UInteger = &H200
    Public Const MAPI_AB_NOMODIFY As UInteger = &H400
    Public Const MAPI_SUCCESS_SUCCESS As UInteger = 0
    Public Const MAPI_USER_ABORT As UInteger = 1
    Public Const MAPI_E_USER_ABORT As UInteger = MAPI_USER_ABORT
    Public Const MAPI_E_FAILURE As UInteger = 2
    Public Const MAPI_E_LOGON_FAILURE As UInteger = 3
    Public Const MAPI_E_LOGIN_FAILURE As UInteger = MAPI_E_LOGON_FAILURE
    Public Const MAPI_E_DISK_FULL As UInteger = 4
    Public Const MAPI_E_INSUFFICIENT_MEMORY As UInteger = 5
    Public Const MAPI_E_ACCESS_DENIED As UInteger = 6
    Public Const MAPI_E_TOO_MANY_SESSIONS As UInteger = 8
    Public Const MAPI_E_TOO_MANY_FILES As UInteger = 9
    Public Const MAPI_E_TOO_MANY_RECIPIENTS As UInteger = 10
    Public Const MAPI_E_ATTACHMENT_NOT_FOUND As UInteger = 11
    Public Const MAPI_E_ATTACHMENT_OPEN_FAILURE As UInteger = 12
    Public Const MAPI_E_ATTACHMENT_WRITE_FAILURE As UInteger = 13
    Public Const MAPI_E_UNKNOWN_RECIPIENT As UInteger = 14
    Public Const MAPI_E_BAD_RECIPTYPE As UInteger = 15
    Public Const MAPI_E_NO_MESSAGES As UInteger = 16
    Public Const MAPI_E_INVALID_MESSAGE As UInteger = 17
    Public Const MAPI_E_TEXT_TOO_LARGE As UInteger = 18
    Public Const MAPI_E_INVALID_SESSION As UInteger = 19
    Public Const MAPI_E_TYPE_NOT_SUPPORTED As UInteger = 20
    Public Const MAPI_E_AMBIGUOS_RECIPIENT As UInteger = 21
    Public Const MAPI_E_AMBIG_RECIP As UInteger = MAPI_E_AMBIGUOS_RECIPIENT
    Public Const MAPI_E_MESSAGE_IN_USE As UInteger = 22
    Public Const MAPI_E_NETWORK_FAILURE As UInteger = 23
    Public Const MAPI_E_INVALID_EDITFIELDS As UInteger = 24
    Public Const MAPI_E_INVALID_RECIPS As UInteger = 25
    Public Const MAPI_E_NOT_SUPPORTED As UInteger = 26
An IntPtr is a pointer to a memory location (unmanaged) that adapts to the platform it is running on (64-bit, etc.) UNLIKE a standard int/Integer. You should always use this type for unmanaged calls that require it, even though an int will appear to work on your development machine.1/13/2008 4:00:13 AM - Damon Carr-72.43.165.29An IntPtr is a pointer to a memory location (unmanaged) that adapts to the platform it is running on (64-bit, etc.) UNLIKE a standard int/Integer. You should always use this type for unmanaged calls that require it, even though an int will appear to work on your development machine.1/13/2008 4:00:13 AM - Damon Carr-72.43.165.29
```
