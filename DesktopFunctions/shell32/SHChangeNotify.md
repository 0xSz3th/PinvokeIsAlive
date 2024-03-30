
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern void SHChangeNotify(HChangeNotifyEventID wEventId, 
                                   HChangeNotifyFlags uFlags, 
                                   IntPtr dwItem1, 
                                   IntPtr dwItem2);
```

## VB Signature:
```cs
<DllImport("shell32.dll")> _
    Shared Sub SHChangeNotify( _
    ByVal wEventID As HChangeNotifyEventID, _
    ByVal uFlags As HChangeNotifyFlags, _
    ByVal dwItem1 As IntPtr, _
    ByVal dwItem2 As IntPtr)
    End Sub
```

## C# Sample Code:
```cs
private void CheckFileAssociation(string ExePath, string FileExt, string Description, string Icon, string ActionName, string FileCommand, string DDECommandString, string App, string Topic)
        {
            RegistryKey RegKey = Registry.ClassesRoot.CreateSubKey("." + FileExt);
            RegKey.SetValue("", FileExt + "File");
            RegKey = Registry.ClassesRoot.CreateSubKey(FileExt + "File");
            RegKey.SetValue("", Description);ssdfsdfsd
            RegKey.SetValue("EditFlags", 0);
            RegKey.SetValue("BrowserFlags", 8);
            RegKey = Registry.ClassesRoot.CreateSubKey(FileExt + @"File\DefaultIcon");
            RegKey.SetValue("", Icon, RegistryValueKind.ExpandString);
            RegKey = Registry.ClassesRoot.CreateSubKey(FileExt + @"File\shell");
            RegKey.SetValue("", FileCommand);
            RegKey = Registry.ClassesRoot.CreateSubKey(FileExt + @"File\shell\" + FileCommand);
            RegKey.SetValue("", ActionName);
            RegKey = Registry.ClassesRoot.CreateSubKey(FileExt + @"File\shell\" + FileCommand + @"\command");
            RegKey.SetValue("", "\"" + ExePath + "\"");
            RegKey = Registry.ClassesRoot.CreateSubKey(FileExt + @"File\shell\" + FileCommand + @"\ddeexec");
            RegKey.SetValue("", DDECommandString);
            RegKey = Registry.ClassesRoot.CreateSubKey(FileExt + @"File\shell\" + FileCommand + @"\ddeexec\Application");
            RegKey.SetValue("", App);
            RegKey = Registry.ClassesRoot.CreateSubKey(FileExt + @"File\shell\" + FileCommand + @"\ddeexec\Topic");
            RegKey.SetValue("", Topic);
            //credits to pinvoke.net
            SHChangeNotify(HChangeNotifyEventID.SHCNE_ASSOCCHANGED, HChangeNotifyFlags.SHCNF_IDLIST, IntPtr.Zero, IntPtr.Zero);
        }

            CheckFileAssociation(
                Application.ExecutablePath, //Application exe path
                "mcl", //Document file extension
                "Celerity Message ControL file", //Document type description
                @"%SystemRoot%\system32\shell32.dll,-152", //Document type icon
                "Open MCL File", //Action name
                "Open", //File command
                "[OpenMCL(\"%1\")]", //DDE command string
                "CelerityEDIToolbox", //Application
                "System"); //Topic
```

## VB Sample Code:
```cs
Private Sub SetFileAssociation( _
    ByVal FileExt As String, _
    ByVal FileClass As String, _
    ByVal Description As String, _
    ByVal Icon As String, _
    ByVal Verb As String, _
    ByVal VerbDescription As String, _
    ByVal Command As String _
    )

    Dim RegKey As RegistryKey = Registry.ClassesRoot.CreateSubKey("." + FileExt)
    RegKey.SetValue("", FileClass)

    Dim RegKeyClass = Registry.ClassesRoot.CreateSubKey(FileClass)
    RegKeyClass.SetValue("", Description)
    If (Not Icon Is Nothing) Then
        RegKey = RegKeyClass.CreateSubKey("DefaultIcon")
        'RegistryValueKind is only supported on CLR 2.0
        'RegKey.SetValue("", Icon, RegistryValueKind.ExpandString)
        RegKey.SetValue("", Icon)
    End If

    RegKey = RegKeyClass.CreateSubKey("shell")
    RegKey = RegKeyClass.CreateSubKey("shell\" + Verb)
    If (Not VerbDescription Is Nothing) Then
        RegKey.SetValue("", VerbDescription)
    End If
    RegKey = RegKeyClass.CreateSubKey("shell\" + Verb + "\command")
    RegKey.SetValue("", Command)

    SHChangeNotify(HChangeNotifyEventID.SHCNE_ASSOCCHANGED, HChangeNotifyFlags.SHCNF_IDLIST, IntPtr.Zero, IntPtr.Zero)
    End Sub
```

## VB Sample Code:
```cs
Dim Path As String = Application.ExecutablePath
    SetFileAssociation( _
        "aaa", _
        "Association.Sample.0", _
        "File Associations Sample", _
        """" + Path + """,0", _
        "open", _
        Nothing, _
        """" + Path + """ ""%1""")
```
