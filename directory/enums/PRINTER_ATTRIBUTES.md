
## C# Definition:
```cs
/// <summary>
/// The printer attributes.
/// </summary>
/// <seealso href="http://msdn.microsoft.com/en-us/library/windows/desktop/dd162845(v=vs.85).aspx"/>
[Flags]
internal enum PRINTER_ATTRIBUTES
{
   /// <summary>
   /// No attribute set.
   /// </summary>
   PRINTER_ATTRIBUTE_NONE = 0,

   /// <summary>
   /// If set, the printer spools and starts printing after the last page is spooled.
   /// If not set and PRINTER_ATTRIBUTE_DIRECT is not set, the printer spools and
   /// prints while spooling.
   /// </summary>
   PRINTER_ATTRIBUTE_QUEUED = 0x1,

   /// <summary>
   /// Job is sent directly to the printer (it is not spooled).
   /// </summary>
   PRINTER_ATTRIBUTE_DIRECT = 0x2,

   /// <summary>
   /// Printer is default printer.
   /// </summary>
   PRINTER_ATTRIBUTE_DEFAULT = 0x4,

   /// <summary>
   /// Printer is shared.
   /// </summary>
   PRINTER_ATTRIBUTE_SHARED = 0x8,

   /// <summary>
   /// Printer is a network printer connection.
   /// </summary>
   PRINTER_ATTRIBUTE_NETWORK = 0x10,

   /// <summary>
   /// Reserved for future use.
   /// </summary>
   PRINTER_ATTRIBUTE_HIDDEN = 0x20,

   /// <summary>
   /// Printer is a local printer.
   /// </summary>
   PRINTER_ATTRIBUTE_LOCAL = 0x40,

   /// <summary>
   /// If set, DevQueryPrint is called. DevQueryPrint may fail if the document 
   /// and printer setups do not match. Setting this flag causes mismatched 
   /// documents to be held in the queue.
   /// </summary>
   PRINTER_ATTRIBUTE_ENABLE_DEVQ = 0x80,

   /// <summary>
   /// If set, jobs are kept after they are printed. If unset, jobs are deleted.
   /// </summary>
   PRINTER_ATTRIBUTE_KEEPPRINTEDJOBS = 0x100,

   /// <summary>
   /// If set and printer is set for print-while-spooling, any jobs that have 
   /// completed spooling are scheduled to print before jobs that have not 
   /// completed spooling.
   /// </summary>
   PRINTER_ATTRIBUTE_DO_COMPLETE_FIRST = 0x200,

   /// <summary>
   /// No description.
   /// </summary>
   PRINTER_ATTRIBUTE_WORK_OFFLINE = 0x400,

   /// <summary>
   /// No description.
   /// </summary>
   PRINTER_ATTRIBUTE_ENABLE_BIDI = 0x800,

   /// <summary>
   /// Indicates that only raw data type print jobs can be spooled.
   /// </summary>
   PRINTER_ATTRIBUTE_RAW_ONLY = 0x1000,

   /// <summary>
   /// Indicates whether the printer is published in the directory service.
   /// </summary>
   PRINTER_ATTRIBUTE_PUBLISHED = 0x2000,

   /// <summary>
   /// <note>In Windows XP and later versions of Windows:</note>
   /// If set, printer is a fax printer. This can only be set by AddPrinter, 
   /// but it can be retrieved by EnumPrinters and GetPrinter.
   /// </summary>
   PRINTER_ATTRIBUTE_FAX = 0x4000,

   /// <summary>
   /// <note>In Windows Server 2003:</note>
   /// Indicates the printer is currently connected through a terminal server.
   /// </summary>
   PRINTER_ATTRIBUTE_TS = 0x8000,

   /// <summary>
   /// <note>In Windows Vista and later versions of Windows:</note>
   /// The printer was installed by using the Push Printer Connections 
   /// user policy. See Print Management Step-by-Step Guide.
   /// </summary>
   PRINTER_ATTRIBUTE_PUSHED_USER = 0x20000,

   /// <summary>
   /// <note>In Windows Vista and later versions of Windows:</note>
   /// The printer was installed by using the Push Printer Connections
   /// computer policy. See Print Management Step-by-Step Guide.
   /// </summary>
   PRINTER_ATTRIBUTE_PUSHED_MACHINE = 0x40000,

   /// <summary>
   /// <note>In Windows Vista and later versions of Windows:</note>
   /// Printer is a per-machine connection.
   /// </summary>
   PRINTER_ATTRIBUTE_MACHINE = 0x80000,

   /// <summary>
   /// <note>In Windows Vista and later versions of Windows:</note>
   /// A computer has connected to this printer and given it a friendly name.
   /// </summary>
   PRINTER_ATTRIBUTE_FRIENDLY_NAME = 0x100000,

   /// <summary>
   /// <note>In Windows Vista and later versions of Windows:</note>
   /// No description.
   /// </summary>
   PRINTER_ATTRIBUTE_TS_GENERIC_DRIVER = 0x200000,
}
```
