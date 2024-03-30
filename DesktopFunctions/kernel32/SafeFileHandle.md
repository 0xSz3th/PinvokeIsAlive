static extern SafeFileHandle CreateFile(string lpFileName, uint dwDesiredAccess,
      uint dwShareMode, IntPtr lpSecurityAttributes, uint dwCreationDisposition,
      uint dwFlagsAndAttributes, IntPtr hTemplateFile);
Private Shared Function CreateFile(ByVal lpFileName As String, ByVal dwDesiredAccess As System.UInt32, ByVal dwShareMode As System.UInt32, ByVal lpSecurityAttributes As IntPtr, ByVal dwCreationDisposition As System.UInt32, ByVal dwFlagsAndAttributes As System.UInt32, ByVal hTemplateFile As IntPtr) As Microsoft.Win32.SafeHandles.SafeFileHandle
The SetLastError API1/26/2016 3:27:33 AM - -124.148.167.58The SetLastError API1/26/2016 3:27:33 AM - -124.148.167.58Click to read this page4/6/2008 7:23:14 AM - anonymous
