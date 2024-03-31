
## C# Definition:
```cs
//IMPORTANT: The order of the methods is critical here. You
    //perform early binding in most cases, so the order of the methods
    //here MUST match the order of their vtable layout (which is determined
    //by their layout in IDL). The interop calls key off the vtable 
    //ordering, not the symbolic names. Therefore, if you switched these 
    //method declarations and tried to call the Exec method on an 
    //IOleCommandTarget interface from your application, it would 
    //translate into a call to the QueryStatus method instead.
    void QueryStatus(
        ref Guid pguidCmdGroup, 
        UInt32 cCmds,
        [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 1)] OLECMD[] prgCmds, 
        ref OLECMDTEXT CmdText);
    void Exec(
        ref Guid pguidCmdGroup, 
        uint nCmdId, 
        uint nCmdExecOpt, 
        ref object pvaIn, 
        ref object pvaOut);
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IOleCommandTarget
   TODO
End Interface
```

## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct OLECMD
    {
        //public UInt32 cmdID;
        //public UInt64 cmdf;
        public uint cmdID;
        public uint cmdf;    // NB: See above note (*)    
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct OLECMDTEXT
    {
        public UInt32 cmdtextf;
        public UInt32 cwActual;
        public UInt32 cwBuf;
        public char rgwz;
    }

    [ComImport, Guid("b722bccb-4e68-101b-a2bc-00aa00404770"), InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IOleCommandTarget
    {

        //IMPORTANT: The order of the methods is critical here. You
        //perform early binding in most cases, so the order of the methods
        //here MUST match the order of their vtable layout (which is determined
        //by their layout in IDL). The interop calls key off the vtable
        //ordering, not the symbolic names. Therefore, if you switched these
        //method declarations and tried to call the Exec method on an
        //IOleCommandTarget interface from your application, it would
        //translate into a call to the QueryStatus method instead.
        [PreserveSig()]
        int QueryStatus([In, MarshalAs(UnmanagedType.Struct)] ref Guid pguidCmdGroup, [MarshalAs(UnmanagedType.U4)] int cCmds, [In, Out]IntPtr prgCmds, [In, Out] IntPtr pCmdText);

        [PreserveSig()]
        int Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdExecOpt, object[] pvaIn, [In, Out, MarshalAs(UnmanagedType.LPArray)] object[] pvaOut);
    }
```

## C# Definition:
```cs
//This attribute demands that all classes derived from the parent class have the specified permission.
    [SecurityPermission(SecurityAction.LinkDemand),
    SecurityPermission(SecurityAction.InheritanceDemand)]

    /// <summary>
    /// This class' methods wrap the IOLE commands.
    /// </summary>
    /// <purpose>
    /// The class makes the calls to functions that handle going from
    /// managed code to native code. The class shows the implementation necessary
    /// for using IOLE Commands.
    /// </purpose>
    public class NativeCommands
    {
        private FormControl _infoPathControl;

        protected const int QUERYFAILED = -1;
        private string lastCommandExecuted;

        /// <summary>
        /// returns the last command that was executed.
        /// </summary>
        public string LastCommandExecuted
        {
            get
            {
                return lastCommandExecuted;
            }
        }

        /// <summary>
        /// InfoPath Form Control object
        /// </summary>
        public FormControl InfoPathControl
        {
            get
            {
                return _infoPathControl;
            }
            set
            {
                _infoPathControl = value;
            }
        }

        #region Structures
        /// <summary>
        /// Struture passed as prgCmds parameter in the QueryStatus method
        /// This structure holds the command to be queried and the result of the query
        /// </summary>
        [StructLayout(LayoutKind.Sequential)]
        public struct OLECMD
        {
            /// <summary>
            /// Command to be queried
            /// </summary>
            private uint cmdID;

            /// <summary>
            /// Result of the query
            /// </summary>
            private uint cmdf;

            /// <summary>
            /// Gets or sets the command to be queried.
            /// </summary>
            public uint CmdId
            {
                get
                {
                    return cmdID;
                }

                set
                {
                    cmdID = value;
                }
            }

            public uint CmdF
            {
                get
                {
                    return cmdf;
                }

                set
                {
                    cmdf = value;
                }
            }
        }
        #endregion

        #region Interfaces

        //import the IOLECommandTarget interface to perform IOLE commands
        //IOLECommandTarget is registered in the registry
        [
        ComImport,
        Guid("B722BCCB-4E68-101B-A2BC-00AA00404770"),
        InterfaceType(ComInterfaceType.InterfaceIsIUnknown)
        ]
        private interface IOleCommandTarget
        {
            /// <summary>
            /// Checks to see if a given command can be executed
            /// </summary>
            /// <param name="pguidCmdGroup">Unique identifier of the command group, NULL to specify the standard group</param>
            /// <param name="cCmds">The number of commands in the prgCmds array</param>
            /// <param name="prgCmds">Array of OLECMD structures that indicate the commands status information is required</param>
            /// <param name="pCmdText">Pointer to name or status of command, NULL indicates this is not necessary</param>
            void QueryStatus(ref Guid pguidCmdGroup, uint cCmds, [MarshalAs(UnmanagedType.LPArray), In, Out] OLECMD[] prgCmds, IntPtr pCmdText);

            /// <summary>
            /// Executes a specified command
            /// </summary>
            /// <param name="pguidCmdGroup">Command group</param>
            /// <param name="nCmdID">Identifier of command to execute</param>
            /// <param name="nCmdExecOpt">Options for executing the command</param>
            /// <param name="pvaIn">Input arguments</param>
            /// <param name="pvaOut">Command output</param>
            void Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdExecOpt, ref object pvaIn, ref object pvaOut);
        }

        #endregion

        #region Enums

        /// <summary>
        /// Designates the type of support provided by an object for the specified command
        /// </summary>
        [FlagsAttribute]
        public enum OleCmdf
        {
            /// <summary>
            /// The command is supported by this object
            /// </summary>
            Supported = 1,
            /// <summary>
            /// The command is available and enabled
            /// </summary>
            Enabled = 2,
            /// <summary>
            /// The command is an on-off toggle and is currently on
            /// </summary>
            Latched = 4,
            /// <summary>
            /// Reserved for future use
            /// </summary>
            Ninched = 8
        }

        #endregion

        #region Query Status
        /// <summary>
        /// Queries whether or not a command can be executed
        /// </summary>
        /// <param name="commandID">ID number of the command to query</param>
        /// <returns>True if command can be performed and false if it cannot</returns>
        public bool QueryCommandStatus(FormControlCommandIds.CommandIds commandId)
        {
            //Create an array for the OLECMD
            OLECMD[] commands = new OLECMD[1];
            commands[0].CmdId = Convert.ToUInt16(commandId,CultureInfo.CurrentCulture);
            commands[0].CmdF = 0;

            QueryCommandStatus(commands);

            //if command is supported and enabled command can be executed
            return (((commands[0].CmdF & (uint)OleCmdf.Supported) != 0) && ((commands[0].CmdF & (uint)OleCmdf.Enabled) != 0));
        }

        /// <summary>
        /// Queries whether or not a command can be executed
        /// </summary>
        /// <param name="commands">Group of commands to be queried</param>
        public void QueryCommandStatus(OLECMD[] commands)
        {
            //Get a IOLECommandTarget object form the ActiveX control
            IOleCommandTarget commandTarget = _infoPathControl.GetOcx() as IOleCommandTarget;

            try
            {
                commandTarget.QueryStatus(ref FormControlCommandIds.CommandGroup, Convert.ToUInt16(commands.Length), commands, IntPtr.Zero);
            }
            catch (Exception ex)
            {
                throw new HostedException("An error occurred while attempting to query commands", ex);
            }
        }
        #endregion

        #region Command Execution

        /// <summary>
        /// Checks whether or not the specified command is on or off
        /// </summary>
        /// <param name="commandID">Command to be executed</param>
        /// <returns>True if command is activated or False if not</returns>
        public bool IsCommandOn(FormControlCommandIds.CommandIds commandId)
        {
            //Create an array for the OLECMD
            OLECMD[] commands = new OLECMD[1];
            commands[0].CmdId = Convert.ToUInt16(commandId,CultureInfo.CurrentCulture);
            commands[0].CmdF = 0;

            QueryCommandStatus(commands);

            return (((commands[0].CmdF & (uint)OleCmdf.Supported) != 0) && ((commands[0].CmdF & (uint)OleCmdf.Enabled) != 0) &&
                ((commands[0].CmdF & (uint)OleCmdf.Latched) != 0));
        }

        /// <summary>
        /// Executes a given command
        /// </summary>
        /// <param name="CommandID">Command to be executed</param>
        /// <returns>Results of executing a command</returns>
        public object ExecuteCommand(FormControlCommandIds.CommandIds commandId)
        {
            return ExecuteCommand(commandId, null);
        }

        /// <summary>
        /// Executes a given command with specified parameters
        /// </summary>
        /// <param name="CommandID">Command to be executed</param>
        /// <param name="vaIn">Input Arguments</param>
        /// <returns>Results of executing the command</returns>
        public object ExecuteCommand(FormControlCommandIds.CommandIds commandId, object vaIn)
        {
            //remember the last command executed
            lastCommandExecuted = commandId.ToString();

            //indicates to Exec call to do the default option
            const int EXECUTE_OPTION_DO_DEFAULT = 0;

            //holds the return result
            object vaOut = null;

            //make sure the command can be executed first
            if (!QueryCommandStatus(commandId))
            {
                return QUERYFAILED;
            }

            // Get the commandTarget from the control
            IOleCommandTarget commandTarget = _infoPathControl.GetOcx() as IOleCommandTarget;

            try
            {
                commandTarget.Exec(ref FormControlCommandIds.CommandGroup, Convert.ToUInt16(commandId,CultureInfo.CurrentCulture),
                    EXECUTE_OPTION_DO_DEFAULT, ref vaIn, ref vaOut);
                return vaOut;
            }
            catch (Exception ex)
            {
                throw new HostedException("An error occurred while executing command " + commandId.ToString(), ex);
            }
        }
        #endregion

    }
```

## C# Definition:
```cs
//This attribute demands that all classes derived from the parent class have the specified permission.
    [SecurityPermission(SecurityAction.LinkDemand),
    SecurityPermission(SecurityAction.InheritanceDemand)]

    /// <summary>
    /// The class makes calls to perform commands against the form control
    /// </summary>
    /// <purpose>
    /// Class is designed to be a central point for executing commands against a form control
    /// In order to use this class a user must provide an instance of a form control.
    /// </purpose>
    public class FormController : NativeCommands
    {
        #region Constructors
        /// <summary>
        /// Commands
        /// </summary>
        public FormController(FormControl parentInfoPathInstance)
        {
            if (parentInfoPathInstance != null)
            {
                InfoPathControl = parentInfoPathInstance;
            }
            else
            {
                InfoPathControl = new FormControl();
            }
        }
        #endregion

        #region Enums and Structs
        /// <summary>
        /// Enumeration of the Interaction type  This will allow different
        /// code paths to be triggered for an action
        /// </summary>
        public enum InteractionType
        {
            /// <summary>
            /// Uses the InfoPath OM
            /// </summary>
            OM = 0,
            /// <summary>
            /// Uses the supported InfoPath IOLECommand
            /// </summary>
            IOLE = 1,
        }

        /// <summary>
        /// Defines the directions a table can have
        /// </summary>
        public struct TableDirectionValues
        {
            public const string NODIRECTION = "none";
            public const string RIGHTTOLEFT = "RTL";
            public const string LEFTTORIGHT = "LTR";
        }

        /// <summary>
        /// Defines the horizontal alignment values for a table
        /// </summary>
        public struct TableHorizontalAlignmentValues
        {
            public const string LEFT = "left";
            public const string CENTER = "center";
            public const string RIGHT = "right";
        }

        /// <summary>
        /// Defines the vertical alignment values for a table
        /// </summary>
        public struct TableVerticalAlignmentValues
        {
            public const string TOP = "top";
            public const string MIDDLE = "middle";
            public const string BOTTOM = "bottom";
        }

        /// <summary>
        /// Defines the picture alignment values for a table
        /// </summary>
        public struct PictureAlignmentValues
        {
            public const string LEFT = "Left";
            public const string RIGHT = "Right";
            public const string INLINE = "inline";
        }

        #endregion

        /// <summary>
        /// Makes sure the command was executed properly
        /// </summary>
        /// <param name="commandResult">The result from executing the command</param>
        /// <returns>The result from executing the command</returns>
        private object ChkResult(object commandResult)
        {
            if ((commandResult !=null) && (commandResult.GetType().Equals(typeof(int))))
            {
                int result = (int)commandResult;
                if (result == QUERYFAILED)
                {
                    throw new NonApplicableCommandException("The command could not be executed at this time because it is not applicable. Command: " + 
                        LastCommandExecuted);
                }
            }
            return commandResult;
        }

        /// <summary>
        /// Makes sure the command was executed properly
        /// </summary>
        /// <param name="commandResult">The result from executing the command</param>
        /// <param name="expectedReturnType">The type of object the command was expected to return</param>
        /// <returns>The result from executing the command</returns>
        private object ChkResult(object commandResult, Type expectedReturnType)
        {
            commandResult = ChkResult(commandResult);

            if ((commandResult!=null) && (!commandResult.GetType().Equals(expectedReturnType)))
            {
                throw new HostedException("Return type was not as expected. Expected type " + expectedReturnType.ToString() +
                    " but received " + commandResult.GetType().ToString() + "\nCommand: " + LastCommandExecuted);
            }
            return commandResult;
        }

        /// <summary>
        /// Enters text into a field
        /// </summary>
        /// <param name="xPath">Field for data</param>
        /// <param name="data">Data to put in the field</param>
        public void EnterData(string xPath, string data)
        {
            if (string.IsNullOrEmpty(xPath))
            {
                throw new InvalidDataException("Parameter 'xPath' must have a value");
            }

            if (string.IsNullOrEmpty(data))
            {
                throw new InvalidDataException("Parameter 'data' must have a value");
            }

            if (IsFormLoaded)
            {
                XPathNavigator field =
                    InfoPathControl.XmlForm.MainDataSource.CreateNavigator().SelectSingleNode(xPath, InfoPathControl.XmlForm.NamespaceManager);
                field.SetValue(data);
            }
            else
            {
                throw new HostedException("No form is currently loaded");
            }
        }

        #region Load Methods

        /// <summary>
        /// Uses a File Open Dialog to get the path and name of an InfoPath xml, xsn or xsf to load
        /// </summary>
        public void Open()
        {
            OpenFileDialog openDialog = new OpenFileDialog();

            //set initial directory the my documents folder
            openDialog.InitialDirectory = System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments);
            openDialog.Filter = "All InfoPath Forms |*.xml;*.xsn|Forms (*.xml)|*.xml,*.xsn|InfoPath Form Templates (*.xsn)|*.xsn|Manifest Files (*.xsf)|*.xsf|All files    (*.*)|*.*";

            //set the default filter = (InfoPath) Forms
            openDialog.FilterIndex = 1;

            //when the user clicks OK, call the Load method of the InfoPath Editor Control object
            if (openDialog.ShowDialog() == DialogResult.OK)
            {
                if (openDialog.FileName.EndsWith(".xsn",StringComparison.OrdinalIgnoreCase) || openDialog.FileName.EndsWith(".xsf",StringComparison.OrdinalIgnoreCase))
                {
                    NewFromFormTemplate(openDialog.FileName);
                }
                else if (openDialog.FileName.EndsWith(".xml",StringComparison.OrdinalIgnoreCase))
                {
                    Open(openDialog.FileName);
                }
                else
                {
                    throw new InvalidFileException("Specified file was not a valid InfoPath File");
                }
            }
            else
            {
                throw new HostedException("Operation was cancelled by the user");
            }
        }

        /// <summary>
        /// Loads a form given the full path and file name
        /// </summary>
        /// <param name="filePath">Full file path and name to an InfoPath xml file</param>
        public void Open(string filePath)
        {
            if (!String.IsNullOrEmpty(filePath))
            {
                try
                {
                    if (!File.Exists(filePath))
                    {
                        throw new InvalidFileException("The file " + filePath + " cannot be found");
                    }

                    InfoPathControl.Open(filePath);
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to open a file", ex);
                }
            }
            else
            {
                throw new InvalidDataException("Parameter 'filePath' must have a value");
            }
        }

        #region OpenThroughStream
        /// <summary>
        /// Uses a Form Open Dialog to load a form.  Loads the instance .xml
        /// into a stream first.
        /// </summary>
        public void OpenThroughStream()
        {
            OpenFileDialog openDialog = new OpenFileDialog();

            openDialog.InitialDirectory = System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments);
            openDialog.Filter = "Forms (*.xml)|*.xml|All files    (*.*)|*.*";

            openDialog.FilterIndex = 1;

            if (openDialog.ShowDialog() == DialogResult.OK)
            {
                if (openDialog.FileName.EndsWith(".xml",StringComparison.OrdinalIgnoreCase))
                {
                    OpenThroughStream(openDialog.FileName);
                }
                else
                {
                    throw new HostedException("Invalid file type. Should be .xml");
                }
            }
            else
            {
                throw new HostedException("Operation was cancelled by the user");
            }
        }

        /// <summary>
        /// Loads an xml from through stream given the full path and file name
        /// </summary>
        /// <param name="fileName">Full path and file name</param>
        public void OpenThroughStream(string fileName)
        {
            if (!String.IsNullOrEmpty(fileName))
            {
                try
                {
                    if (!File.Exists(fileName))
                    {
                        throw new InvalidFileException("The file " + fileName + " cannot be found");
                    }

                    XmlDocument tempXmlDoc = new XmlDocument();
                    tempXmlDoc.Load(fileName);

                    MemoryStream tempCoreStream = new MemoryStream();
                    tempXmlDoc.Save(tempCoreStream);

                    InfoPathControl.Open(tempCoreStream);

                    tempCoreStream.Close();
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to open a file", ex);
                }
            }
            else
            {
                throw new InvalidDataException("Parameter 'fileName' must contain a value");
            }
        }
        #endregion
```

## C# Definition:
```cs
/// <summary>
        /// Opens an InfoPath form template in the Editor
        /// </summary>
        /// <param name="filePath">Full path and file name of the .xsf or .xsn file</param>
        public void NewFromFormTemplate(string filePath)
        {
            if (!String.IsNullOrEmpty(filePath))
            {
                try
                {
                    if (!File.Exists(filePath))
                    {
                        throw new InvalidFileException("The file " + filePath + " cannot be found");
                    }
                    InfoPathControl.NewFromFormTemplate(filePath);
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to open a file", ex);
                }
            }
            else
            {
                throw new InvalidDataException("Parameter 'filePath' must contain a value");
            }
        }

        /// <summary>
        /// Uses Form Open Dialogs to get an instance .xml and a solution .xsn 
        /// to load.  The .xml is loaded into a stream first.
        /// </summary>
        public void NewFromFormTemplateWithData()
        {
            string xmlFile = string.Empty;
            string xsnFile = string.Empty;

            OpenFileDialog openDialog = new OpenFileDialog();

            openDialog.InitialDirectory = System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments);

            //get instance xml file
            openDialog.Title = "Select instance .xml file.";
            openDialog.Filter = "Forms (*.xml)|*.xml|All files    (*.*)|*.*";
            if (openDialog.ShowDialog() == DialogResult.OK)
            {
                if (openDialog.FileName.EndsWith(".xml",StringComparison.OrdinalIgnoreCase))
                {
                    xmlFile = openDialog.FileName;
                }
                else
                {
                    throw new InvalidFileException("Selected file " + openDialog.FileName + " was not an XML file");
                }
```

## C# Definition:
```cs
//get form template xsn
                openDialog.Title = "Select form tempalte .xsn.";
                openDialog.Filter = "Form Templates (*.xsn)|*.xsn|All files    (*.*)|*.*";
                if (openDialog.ShowDialog() == DialogResult.OK)
                {
                    if (openDialog.FileName.EndsWith(".xsn",StringComparison.OrdinalIgnoreCase))
                    {
                        xsnFile = openDialog.FileName;
                    }
                    else
                    {
                        throw new HostedException("Selected file " + openDialog.FileName + " was not an XSN file");
                    }
                }
            }

            //Load files provided user did not cancel any option
            if (!(string.IsNullOrEmpty(xmlFile)) && !(string.IsNullOrEmpty(xsnFile)))
            {
                NewFromFormTemplateWithData(xmlFile, xsnFile);
            }
            else
            {
                throw new HostedException("Operation was cancelled by user");
            }
        }

        /// <summary>
        /// Load an XSN using data specified by in an xml file
        /// </summary>
        /// <param name="xmlFile">Data to open xsn with</param>
        /// <param name="xsnFile">XSN file to open</param>
        public void NewFromFormTemplateWithData(string xmlFile, string xsnFile)
        {
            if (String.IsNullOrEmpty(xmlFile))
            {
                throw new InvalidDataException("Parameter 'xmlFile' must have a value");
            }

            if (String.IsNullOrEmpty(xsnFile))
            {
                throw new InvalidDataException("Parameter 'xsnFile' must have a value");
            }

            if (!File.Exists(xmlFile))
            {
                throw new InvalidFileException("The file " + xmlFile + " cannot be found");
            }

            if (!File.Exists(xsnFile))
            {
                throw new InvalidFileException("The file " + xsnFile + " cannot be found");
            }

            try
            {
                XmlDocument tempXmlDoc = new XmlDocument();
                tempXmlDoc.Load(xmlFile);

                MemoryStream tempCoreStream = new MemoryStream();
                tempXmlDoc.Save(tempCoreStream);

                InfoPathControl.NewFromFormTemplate(xsnFile, tempCoreStream, XmlFormOpenMode.Default);

                tempCoreStream.Close();
            }
            catch (Exception ex)
            {
                throw new HostedException("An error occurred while attempting to open a file", ex);
            }
        }

        #endregion

        #region Save
        /// <summary>
        /// Saves the currently opened document
        /// </summary>
        /// <param name="interactionType">OM or IOLE</param>
        public void Save(InteractionType interactionType)
        {
            switch (interactionType)
            {
                case InteractionType.OM:
                    if (IsFormLoaded)
                    {
                        try
                        {
                            InfoPathControl.XmlForm.Save();
                        }
                        catch(Exception ex)
                        {
                            throw new HostedException("An error occurred while attempting to save this form", ex);
                        }
                    }
                    break;
                case InteractionType.IOLE:
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Save));
                    break;
                default:
                    throw new HostedException("Invalid InteractionType.");
            }
        }

        /// <summary>
        /// Opens the Save As dialog
        /// </summary>
        /// <param name="interactionType">IOLE or OM</param>
        public void SaveAs(InteractionType interactionType)
        {
            switch (interactionType)
            {
                case InteractionType.OM:
                    if (IsFormLoaded)
                    {
                        SaveFileDialog saveFileDialog = new SaveFileDialog();

                        saveFileDialog.InitialDirectory = System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments);

                        saveFileDialog.Filter = "Forms (*.xml)|*.xml|All files (*.*)|*.*";

                        saveFileDialog.FilterIndex = 1;

                        if (saveFileDialog.ShowDialog() == DialogResult.OK)
                        {
                            SaveAs(saveFileDialog.FileName);
                        }
                    }
                    break;
                case InteractionType.IOLE:
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SaveAs));
                    break;
                default:
                    throw new HostedException("Invalid InteractionType.");
            }
        }

        /// <summary>
        /// Does a save as using the object model given the save location
        /// </summary>
        /// <param name="savePath">Location to save the file</param>
        public void SaveAs(string savePath)
        {
            if (String.IsNullOrEmpty(savePath))
            {
                throw new InvalidDataException("Parameter 'savePath' must have a value");
            }

            try
            {
                if (savePath.EndsWith(".xml",StringComparison.OrdinalIgnoreCase))
                {
                    InfoPathControl.XmlForm.SaveAs(savePath);
                }
                else
                {
                    InfoPathControl.XmlForm.SaveAs(savePath + ".xml");
                }
            }
            catch (Exception ex)
            {
                throw new HostedException("An error occurred while attempting to save this form", ex);
            }
        }

        #endregion

        #region Print
        /// <summary>
        /// Prints the current view. Print Dialog does not appear and therefore a document 
        /// will be printed.with the default printer settings
        /// </summary>
        public void Print()
        {
            if (IsFormLoaded)
            {
                try
                {
                    InfoPathControl.XmlForm.Print();
                    //NOTE: XmlForm.Print(true) will NOT show the print dialog.
                    //The print dialog is not supported in hosting scenarios
                }
                catch(Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to print this form", ex);
                }
            }
        }
        #endregion

        #region Close
        /// <summary>
        /// Closes an XMLForm in the form control
        /// </summary>
        /// <param name="interactionType">Execute through IOLE or OM</param>
        public void Close(InteractionType interactionType)
        {
            // Check to make sure there is a document loaded before    
            // trying to close it
            if (IsFormLoaded)
            {
                switch (interactionType)
                {
                    case InteractionType.OM:
                        try
                        {
                            InfoPathControl.XmlForm.Close();
                        }
                        catch (Exception ex)
                        {
                            throw new HostedException("An error occurred while attempting to close this form", ex);
                        }
                        break;
                    case InteractionType.IOLE:
                        ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Close));
                        break;
                    default:
                        throw new HostedException("Invalid InteractionType.");
                }
            }
        }
        #endregion

        #region Font Formatting

        #region Bold

        /// <summary>
        /// Sets/Unsets the formatting of the selected text to bold
        /// </summary>
        public void ToggleFontFormattingBold()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingBold));
        }

        #endregion

        #region Italic
        ///    <summary>
        ///    Sets/Unsets the formatting of the selected text to Italics
        ///    </summary>
        public void ToggleFontFormattingItalic()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingItalic));
        }

        #endregion

        #region Underline

        ///    <summary>
        ///    Sets/Unsets the formatting of the selected text to be Underlined
        ///    </summary>
        public void ToggleFontFormattingUnderline()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingUnderline));
        }
        #endregion

        #region Strikethrough
        ///    <summary>
        ///    Sets/Unsets the formatting of the selected text to be strikethrough
        ///    </summary>
        public void ToggleFontFormattingStrikethrough()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingStrikethrough));
        }
        #endregion

        #region Superscript
        ///    <summary>
        ///    Sets the formatting of the selected text to be superscipt
        ///    </summary>
        public void ToggleFontFormattingSuperscript()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingSuperscript));
        }
        #endregion

        #region Subscript
        ///    <summary>
        ///    Sets/Unsets the formatting of the selected text to subscript
        ///    </summary>
        public void ToggleFontFormattingSubscript()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingSubscript));
        }

        #endregion

        #region IncreaseFontSizeBy2
        ///    <summary>
        ///    Increases the font size of the selected text by 2
        ///    </summary>
        public void IncreaseFontSizeBy2()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.IncreaseFontSizeBy2));
        }
        #endregion

        #region DecreaseFontSizeBy2
        ///    <summary>
        ///    Decreases the font size of the selected text by 2
        ///    </summary>
        public void DecreaseFontSizeBy2()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.DecreaseFontSizeBy2));
        }
        #endregion

        #region ClearFontFormatting
        ///    <summary>
        ///    Clears font formatting of the selected text
        ///    </summary>
        public void ClearFontFormatting()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ClearFontFormatting));
        }
        #endregion

        #region Headings
        ///    <summary>
        ///    Sets the font formatting of the selected text to InfoPath's setting for heading 1
        ///    </summary>
        public void SetFontFormattingHeading1()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingHeading1));
        }

        ///    <summary>
        ///Sets the font formatting of the selected text to InfoPath's setting for heading 2
        ///    </summary>
        public void SetFontFormattingHeading2()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingHeading2));
        }

        ///    <summary>
        ///    Sets the font formatting of the selected text to InfoPath's setting for heading 3
        ///    </summary>
        public void SetFontFormattingHeading3()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingHeading3));
        }

        ///    <summary>
        ///    Sets the font formatting of the selected text to InfoPath's setting for heading 4
        ///    </summary>
        public void SetFontFormattingHeading4()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingHeading4));
        }

        ///    <summary>
        ///    Sets the font formatting of the selected text to InfoPath's setting for heading 5
        ///    </summary>
        public void SetFontFormattingHeading5()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingHeading5));
        }

        ///    <summary>
        ///    Sets the font formatting of the selected text to InfoPath's setting for heading 6
        ///    </summary>
        public void SetFontFormattingHeading6()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingHeading6));
        }

        ///    <summary>
        ///    Sets the font formatting of the selected text to InfoPath's setting for normal
        ///    </summary>
        public void SetFontFormattingNormal()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFontFormattingNormal));
        }

        #endregion

        #region Font
        /// <summary>
        /// Gets the number of fonts in InfoPath's font list
        /// </summary>
        ///<returns>numbers of fonts available</returns>
        public int FontsAvailableCount
        {
            get
            {
                return Convert.ToInt32(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetFontsAvailableCount), typeof(int)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Gets the name of a font from InfoPath's font combobox at a user specified index
        /// </summary>
        /// <param name="index">index of the font</param>
        /// <returns>The name of the font, empty if index is invalid</returns>
        public string GetFontAt(int index)
        {
            if (index >= 0 && index < FontsAvailableCount)
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetFontAvailableByIndex, index), typeof(string)),CultureInfo.CurrentCulture
                    );
            }
            else
            {
                throw new InvalidDataException("Index is not in a valid range");
            }
        }
```

## C# Definition:
```cs
/// <summary>
        /// Sets/Gets the font of the currenty selected text
        /// </summary>
        /// <returns>The name of the font of the selected text</returns>
        public string SelectedTextFont
        {
            get
            {
                    return Convert.ToString(
                        ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedTextFont),typeof(string)),CultureInfo.CurrentCulture
                        );

            }

            set
            {
                if (!String.IsNullOrEmpty(value))
                {
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedTextFont, value));
                }
            }
        }
        #endregion

        #region FontSize
        /// <summary>
        /// Gets the number of font sizes in InfoPath's font size lists
        /// </summary>
        /// <returns>The number of font sizes available</returns>
        public int FontSizesAvailableCount
        {
            get
            {
                return Convert.ToInt32(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetFontSizesAvailableCount),typeof(int)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Gets the value of a font size from InfoPath's font sizes combobox at a user specified index
        /// </summary>
        /// <param name="index">Index of the requested font size</param>
        /// <returns>The font size at the specified index</returns>
        public string GetFontSizeAt(int index)
        {
            if (index >= 0 && index < FontSizesAvailableCount)
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetFontSizeAvailableByIndex, index), typeof(string)),CultureInfo.CurrentCulture
                    );
            }
            else
            {
                throw new InvalidDataException("Index is not in a valid range");
            }
        }

        /// <summary>
        /// Sets/Gets the font size of the currently selected text
        /// </summary>
        /// <returns>The name of the font size of the selected text</returns>
        public string SelectedTextFontSize
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedTextFontSize), typeof(string)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                if (!String.IsNullOrEmpty(value))
                {
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedTextFontSize, value));
                }
            }
        }

        #endregion

        #region Font Color
        /// <summary>
        /// Sets/Gets the font color of the selected text
        /// </summary>
        /// <returns>The current font color</returns>
        public Color FontColor
        {
            get
            {
                try
                {
                    return ColorTranslator.FromOle(Convert.ToInt32(
                            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedTextFontColor), typeof(int)), CultureInfo.CurrentCulture
                            ));
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to get the font color", ex);
                }
            }

            set
            {
                UInt32 vaIn;
                try
                {
                    vaIn = Convert.ToUInt32(System.Drawing.ColorTranslator.ToOle(value));
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to set the font color", ex);
                }

                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedTextFontColor, vaIn));

            }
        }

        /// <summary>
        /// Gets InfoPath's default font color
        /// </summary>
        /// <returns>The default font color</returns>
        public Color DefaultFontColor
        {
            get
            {
                try
                {
                    return ColorTranslator.FromOle(Convert.ToInt32(
                        ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetDefaultFontColor), typeof(int)),CultureInfo.CurrentCulture
                        ));
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to get the default font color", ex);
                }
            }
        }

        #endregion

        #region HighlightColor
        /// <summary>
        /// Sets/Gets the highlight color of the selected text
        /// </summary>
        /// <returns type="Color">The current highlight color</returns>
        public Color HighlightColor
        {
            get
            {
                try
                {
                    return ColorTranslator.FromOle(Convert.ToInt32(
                        ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedTextHighlightColor), typeof(int)),CultureInfo.CurrentCulture
                        ));
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to get the highlight color", ex);
                }
            }

            set
            {
                UInt32 vaIn;
                try
                {
                    vaIn = Convert.ToUInt32(System.Drawing.ColorTranslator.ToOle(value));
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to set the highlight color", ex);
                }
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedTextHighlightColor, vaIn));
            }
        }

        /// <summary>
        /// Gets InfoPath's default highlight color
        /// </summary>
        /// <returns type="Color">The default highlight color</returns>
        public Color DefaultHighlightColor
        {
            get
            {
                try
                {
                    return ColorTranslator.FromOle(Convert.ToInt32(
                        ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetDefaultHighlightColor), typeof(int)),CultureInfo.CurrentCulture
                        ));
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to get the default highlight color", ex);
                }
            }
        }
        #endregion

        #endregion

        #region Paragraph settings

        #region AlignLeft
        /// <summary>
        /// Aligns the selected paragraph to the left
        /// </summary>
        public void AlignTextLeft()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.AlignTextLeft));
        }

        #endregion

        #region AlignCenter
        /// <summary>
        /// Aligns the selected paragraph to the center
        /// </summary>
        public void AlignTextCenter()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.AlignTextCenter));
        }

        #endregion

        #region AlignRight
        ///    <summary>
        ///    Aligns the selected paragraph to the right
        ///    </summary>
        public void AlignTextRight()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.AlignTextRight));
        }

        #endregion

        #region AlignJustify
        ///    <summary>
        ///    Justifies the selected paragraph
        ///    </summary>
        public void AlignTextJustify()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.AlignTextJustify));
        }

        #endregion

        #region Increase Indent
        ///    <summary>
        ///    Increases indentation of the selected paragraph
        ///    </summary>
        public void IncreaseIndent()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.IncreaseIndent));
        }
        #endregion

        #region Decrease Indent
        ///    <summary>
        ///    Decreases indentation of the selected paragraph
        ///    </summary>
        public void DecreaseIndent()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.DecreaseIndent));
        }
        #endregion

        #region Single Line Spacing
        ///    <summary>
        ///    Sets the line spacing to 1.0
        ///    </summary>
        public void SetSingleLineSpacing()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSingleLineSpacing));
        }

        #endregion

        #region Double Line Spacing
        ///    <summary>
        ///    Sets the line spacing to 2.0
        ///    </summary>
        public void SetDoubleLineSpacing()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetDoubleLineSpacing));
        }

        #endregion

        #region 1.5 Line Spacing
        ///    <summary>
        ///    Sets the line spacing to 1.5
        ///    </summary>
        public void Set15LineSpacing()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Set15LineSpacing));
        }

        #endregion

        #region Background Color
        /// <summary>
        /// Gets the background color of the selected text
        /// </summary>
        /// <returns type="Color">the current background color</returns>
        public Color BackgroundColor
        {
            get
            {
                try
                {
                    return ColorTranslator.FromOle(Convert.ToInt32(
                        ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedTextBackgroundColor)),CultureInfo.CurrentCulture
                        ));
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to get the background color", ex);
                }
            }

            set
            {
                UInt32 vaIn;
                try
                {
                    vaIn = Convert.ToUInt32(System.Drawing.ColorTranslator.ToOle(value));
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to set the background color", ex);
                }
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedTextBackgroundColor, vaIn));
            }
        }
        #endregion

        #endregion

        #region Editing

        #region Undo
        ///    <summary>
        ///    Un-does the last action
        ///    </summary>
        public void Undo()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Undo));
        }
        #endregion

        #region Redo
        ///    <summary>
        ///    Re-does the last action
        ///    </summary>
        public void Redo()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Redo));
        }
        #endregion

        #region Cut
        ///    <summary>
        ///    Cuts the selected text and copies it to the clipboard
        ///    </summary>
        public void Cut()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Cut));
        }
        #endregion

        #region Copy
        ///    <summary>
        ///    Copies the selected text to the clipboard
        ///    </summary>
        public void Copy()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Copy));
        }
        #endregion

        #region Paste
        ///    <summary>
        ///    Pastes the copied or cut text into the selected control
        ///    </summary>
        public void Paste()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Paste));
        }
        #endregion

        #region Select All
        ///    <summary>
        ///    Selects all of the text in a control
        ///    </summary>
        public void SelectAll()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectAll));
        }

        #endregion

        #region Format Painter
        /// <summary>
        /// Applies the current formatting to other text
        /// </summary>
        public void FormatPainter()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.FormatPainterCopyFormatting));
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.FormatPainterApplyFormatting));
        }

        /// <summary>
        /// Applies the current formatting to other text with the brush remaining after each paste
        /// </summary>
        public void FormatPainterPersistent()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.FormatPainterCopyFormattingPersistent));
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.FormatPainterApplyFormattingPersistent));
        }
        #endregion

        #region Find and Replace

        /// <summary>
        /// Sets/Gets whether or not the use wildcards option is turned on
        /// </summary>
        /// <returns>True if use wildcards is on, otherwise false</returns>
        public bool FindReplaceOptionUseWildcardsOn
        {
            get
            {
                return IsCommandOn(FormControlCommandIds.CommandIds.SetFindReplaceOptionUseWildcards);
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFindReplaceOptionUseWildcards, value));
            }
        }

        /// <summary>
        /// Sets/Gets whether or not the match case option is turned on
        /// </summary>
        /// <returns>True if match case is on, otherwise false</returns>
        public bool FindReplaceOptionMatchCaseOn
        {
            get
            {
                return IsCommandOn(FormControlCommandIds.CommandIds.SetFindReplaceOptionMatchCase);
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFindReplaceOptionMatchCase, value));
            }
        }

        /// <summary>
        /// Sets/Gets whether or not the use whole words only option is turned on
        /// </summary>
        /// <returns>True if whole words only is on, otherwise false</returns>
        public bool FindReplaceOptionWholeWordsOnlyOn
        {
            get
            {
                return IsCommandOn(FormControlCommandIds.CommandIds.SetFindReplaceOptionWholeWordOnly);
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFindReplaceOptionWholeWordOnly, value));
            }

        }

        /// <summary>
        /// Sets/Gets the search direction
        /// </summary>
        /// <returns>1 for up, o for down</returns>
        public int FindReplaceOptionSearchDirection
        {
            get
            {
                return Convert.ToInt32(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetFindReplaceOptionSearchDirection),typeof(int)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFindReplaceOptionSearchDirection, value));
            }
        }

        /// <summary>
        /// Gets the result of the find/replace action
        /// </summary>
        /// <returns>The result of the find operation</returns>
        public int FindReplaceResult
        {
            get
            {
                return Convert.ToInt32(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetFindReplaceState),typeof(int)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Sets/Gets the string being searched for
        /// </summary>
        /// <returns>The string being searched for</returns>
        public string FindString
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetFindString),typeof(string)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetFindString, value));
            }
        }

        /// <summary>
        /// Sets/Gets the string replacing the search string
        /// </summary>
        /// <returns>The replacement string</returns>
        public string ReplaceString
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetReplaceWithString),typeof(string)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetReplaceWithString, value));
            }
        }
        /// <summary>
        /// Finds the next instance of the search string in the document
        /// </summary>
        public void FindNext()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.FindReplaceFindNext));
        }

        ///    <summary>
        ///    Replaces the currently selected search string instance
        ///    </summary>
        ///    <param name="ReplaceString">string to replace selected string</param>
        public void Replace()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Replace));
        }

        ///    <summary>
        ///    Replaces all matching instances of the find parameter
        ///    </summary>
        ///    <param name="ReplaceString">string to replace find string with</param>
        public void ReplaceAll()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ReplaceAll));
        }

        #endregion

        #endregion

        #region Bulletts and Numbering

        #region ClearBulletList
        ///    <summary>
        ///    Remove the bullets from the selected line(s)
        ///    </summary>
        public void ClearBulletedList()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ClearBulletedList));
        }

        ///    <summary>
        ///    Removes the numbered list from the selected line(s)
        ///    </summary>
        public void ClearNumberedList()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ClearNumberedList));
        }
        #endregion

        #region Insert Numbered and Bulleted List
        ///    <summary>
        ///    Inserts/Removes a numbered list for the current selection
        ///    </summary>
        public void InsertNumberedList()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertNumberedList));
        }

        ///    <summary>
        ///    Inserts/Removes a bulleted list for the current selection
        ///    </summary>
        public void InsertBulletedList()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertBulletedList));
        }
        #endregion

        #region Insert NumberList Decimal
        ///    <summary>
        ///    Inserts a numbered list using decimal numbers
        ///    </summary>
        public void InsertNumberedListDecimal()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertNumberedListDecimal));
        }

        #endregion

        #region InsertNumberedListRomanUppercase
        ///    <summary>
        ///    Inserts a numbered list using upper case roman numeral numbers
        ///    </summary>
        public void InsertNumberedListRomanUppercase()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertNumberedListRomanUppercase));
        }
        #endregion

        #region InsertNumberedListRomanLowercase
        ///    <summary>
        ///    Inserts a numbered list using lower case roman numeral numbers
        ///    </summary>
        public void InsertNumberedListRomanLowercase()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertNumberedListRomanLowercase));
        }

        #endregion

        #region InsertNumberedListAlphaUppercase
        ///    <summary>
        ///    Inserts an numbered list using uppercase alpha numeric numbers
        ///    </summary>
        public void InsertNumberedListAlphaUppercase()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertNumberedListAlphaUppercase));
        }

        #endregion

        #region InsertNumberedListAlphalowercase
        ///    <summary>
        ///    Inserts a numbered list using lowercase alpha numeric numbers
        ///    </summary>
        public void InsertNumberedListAlphaLowercase()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertNumberedListAlphaLowercase));
        }
        #endregion

        #region InsertBulletListSolidCircle
        ///    <summary>
        ///    Inserts a bulleted list with solid circles
        ///    </summary>
        public void InsertBulletedListSolidCircle()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertBulletedList));
        }

        #endregion

        #region InsertBulletListEmptyCircle
        ///    <summary>
        ///    Inserts a bulleted list with empty circles
        ///    </summary>
        public void InsertBulletedListEmptyCircle()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertBulletedListEmptyCircle));
        }

        #endregion

        #region InsertBulletListSolidSquare
        ///    <summary>
        ///    Inserts a bulleted list with solid squares
        ///    </summary>
        public void InsertBulletedListSolidSquare()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertBulletedListSolidSquare));
        }

        #endregion

        #endregion

        #region Table Settings
        #region Draw Table
        ///    <summary>
        ///    Activates/Deactivates draw pen which is used to create a table
        ///    </summary>
        public void ToggleDrawTable()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.DrawTable));
        }

        #endregion

        #region Erase Table
        ///    <summary>
        ///    Activates/Deactivates the eraser for erasing a table
        ///    </summary>
        public void ToggleEraseTable()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.EraseTable));
        }

        #endregion

        #region Insert and Delete Table
        /// <summary>
        /// Inserts a table into a supported control
        /// </summary>
        /// <param name="numRows">Number of rows the table should have</param>
        /// <param name="numCols">Number of columns the table should have</param>
        public void InsertTable(int rows, int columns)
        {
            if ((rows > 0) && (columns > 0))
            {
                object[] vaIn = new object[2];
                vaIn[0] = rows;
                vaIn[1] = columns;

                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertTable, vaIn));
            }
            else
            {
                throw new InvalidDataException("The number of rows and columns must be greater than zero.");
            }
        }

        /// <summary>
        /// Deletes the selected table
        /// </summary>
        public void DeleteSelectedTable()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.DeleteSelectedTable));
        }
        #endregion

        #region Select a Table
        /// <summary>
        /// Selects all of the current table
        /// </summary>
        public void SelectTable()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectTable));
        }
        #endregion

        #region Insert columns and rows
        /// <summary>
        /// Inserts a column to the left of the currently focused column
        /// </summary>
        public void InsertColumnLeft()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertColumnLeft));
        }

        /// <summary>
        /// Inserts a column to the right of the currently focused column
        /// </summary>
        public void InsertColumnRight()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertColumnRight));
        }

        /// <summary>
        /// Inserts a row above the currently focused row
        /// </summary>
        public void InsertRowAbove()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertRowAbove));
        }

        /// <summary>
        /// Inserts a row below the currently focused row
        /// </summary>
        public void InsertRowBelow()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertRowBelow));
        }
        #endregion

        #region Delete columns and rows
        /// <summary>
        /// Deletes the selected columns
        /// </summary>
        public void DeleteSelectedColumns()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.DeleteSelectedColumns));
        }

        /// <summary>
        /// Deletes the selected rows
        /// </summary>
        public void DeleteSelectedRows()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.DeleteSelectedRows));
        }
        #endregion

        #region Select columns and rows
        /// <summary>
        /// Selects all of the current column
        /// </summary>
        public void SelectColumn()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectColumns));
        }

        /// <summary>
        /// Selects the column before the column with the current focus
        /// </summary>
        public void SelectPreviousColumn()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectPreviousColumn));
        }

        /// <summary>
        /// Selects the column after the column with the current focus
        /// </summary>
        public void SelectNextColumn()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectNextColumn));
        }

        /// <summary>
        /// Selects all of the current row
        /// </summary>
        public void SelectRow()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectRows));
        }

        /// <summary>
        /// Selects the row before the row with the current focus
        /// </summary>
        public void SelectPreviousRow()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectPreviousRow));
        }

        /// <summary>
        /// Selects the row after the row with the current focus
        /// </summary>
        public void SelectNextRow()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectNextRow));
        }
        #endregion

        #region Cells
        /// <summary>
        /// Selects the entire current cell
        /// </summary>
        public void SelectCell()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectCell));
        }

        /// <summary>
        /// Combines two or more cells of a table
        /// </summary>
        public void MergeCells()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.MergeCells));
        }

        /// <summary>
        /// Splits Cells into different proportions
        /// </summary>
        /// <param name="numCols">Number of columns to split into</param>
        /// <param name="numRows">Number of rows to split cells into</param>
        /// <param name="merge">Flag indicating cells should be merged/not merged before splitting</param>
        public void SplitCells(decimal columns, decimal rows, bool merge)
        {
            if ((rows > 0) && (columns > 0))
            {
                object[] vaIn = new object[3];
                vaIn[0] = columns.ToString(CultureInfo.CurrentCulture);
                vaIn[1] = rows.ToString(CultureInfo.CurrentCulture);
                vaIn[2] = merge;

                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SplitCells, vaIn));
            }
            else
            {
                throw new InvalidDataException("The number of rows and columns must be greater than zero");
            }
        }

        #region Cell Alignment
        /// <summary>
        /// Sets the alignment of the selected cell to be at the top
        /// </summary>
        public void SetSelectedCellAlignmentTop()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedCellAlignmentTop));
        }

        /// <summary>
        /// Sets the alignment of the selected cell to be in the middle
        /// </summary>
        public void SetSelectedCellAlignmentMiddle()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedCellAlignmentMiddle));
        }

        /// <summary>
        /// Sets the alignment of the selected cell to be at the bottom
        /// </summary>
        public void SetSelectedCellAlignmentBottom()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedCellAlignmentBottom));
        }

        /// <summary>
        /// Gets the vertical alignment of the selected cell
        /// </summary>
        /// <return type="string">vertical alignment value (top,middle,bottom)</return>
        public string SelectedCellVerticalAlignment
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedCellVerticalAlignment),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }
        #endregion

        #region Table cell padding
        /// <summary>
        /// Sets the padding of selected cells
        /// </summary>
        /// <param name="padTop">padding to the top</param>
        /// <param name="padRight">padding to the right</param>
        /// <param name="padBottom">padding to the bottom</param>
        /// <param name="padLeft">padding to the left</param>
        public void SetSelectedCellPadding(string padTop, string padRight, string padBottom, string padLeft)
        {
            if (!String.IsNullOrEmpty(padTop) && !String.IsNullOrEmpty(padRight) && !String.IsNullOrEmpty(padBottom)
                && !String.IsNullOrEmpty(padLeft))
            {
                object[] vaIn = new object[4];
                vaIn[0] = padTop;
                vaIn[1] = padRight;
                vaIn[2] = padBottom;
                vaIn[3] = padLeft;

                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedCellPadding, vaIn));
            }
            else
            {
                throw new InvalidDataException("One or more parameters is invalid");
            }
        }

        /// <summary>
        /// Gets the top padding of the selected cell
        /// </summary>
        /// <returns>The value for the top padding. Includes unit</returns>
        public string SelectedCellTopPadding
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedCellTopPadding),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Gets the right padding of the selected cell
        /// </summary>
        /// <returns>The value for the right padding. Includes unit</returns>
        public string SelectedCellRightPadding
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedCellRightPadding),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Gets the bottom padding of the selected cell
        /// </summary>
        /// <returns>The value for the bottom padding. Includes unit</returns>
        public string SelectedCellBottomPadding
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedCellBottomPadding),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Gets the left padding of the selected cell
        /// </summary>
        /// <returns>The value for the left padding. Includes unit</returns>
        public string SelectedCellLeftPadding
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedCellLeftPadding),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }
        #endregion

        #endregion

        #region Table Alignment
        /// <summary>
        /// Sets/Gets the alignment of the table
        /// </summary>
        /// <return>string (left, center, right)</return>
        public string TableHorizontalAlignment
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetTableHorizontalAlignment),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetTableHorizontalAlignment, value));
            }
        }
        #endregion

        #region Table Direction
        /// <summary>
        /// Sets/Gets the direction of the table
        /// </summary>
        /// <return type=string>value of direction ("LTR" (Left To Right) or "RTL" (Right To Left))</return>
        public string TableDirection
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetTableDirection),typeof(string)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetTableDirection, value));
            }
        }
        #endregion

        #region Row height and column width

        /// <summary>
        /// Sets/Gets the height of the selected row
        /// </summary>
        /// <returns>The height of the selected row with units</returns>
        public string RowHeight
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedRowHeight),typeof(string)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedRowHeight, value));
            }
        }

        /// <summary>
        /// Sets/Gets the width of the selected column
        /// </summary>
        /// <returns>The width of the selected column with units</returns>
        public string ColumnWidth
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSelectedColumnWidth),typeof(string)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSelectedColumnWidth, value));
            }
        }
        #endregion

        #region Row and column properties options
        /// <summary>
        /// Checks if there is a row below the currently selected row
        /// </summary>
        public bool IsNextRowExist
        {
            get
            {
                return IsCommandOn(FormControlCommandIds.CommandIds.SelectNextRow);
            }
        }

        /// <summary>
        /// Checks if there is a row above the currently selected row
        /// </summary>
        public bool IsPreviousRowExist
        {
            get
            {
                return IsCommandOn(FormControlCommandIds.CommandIds.SelectPreviousRow);
            }
        }

        /// <summary>
        /// Selects the next row in the table
        /// </summary>
        public void GotoNextRow()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectNextRow));
        }

        /// <summary>
        /// Selects the previous row in the table
        /// </summary>
        public void GotoPreviousRow()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectPreviousRow));
        }

        /// <summary>
        /// Checks if there is a column right of the currently selected column
        /// </summary>
        public bool IsNextColumnExist
        {
            get
            {
                return IsCommandOn(FormControlCommandIds.CommandIds.SelectNextColumn);
            }
        }

        /// <summary>
        /// Checks if there is a column left of the currently selected column
        /// </summary>
        public bool IsPreviousColumnExist
        {
            get
            {
                return IsCommandOn(FormControlCommandIds.CommandIds.SelectPreviousColumn);
            }
        }

        /// <summary>
        /// Selects the next column in the table
        /// </summary>
        public void GotoNextColumn()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectNextColumn));
        }

        /// <summary>
        /// Selects the previous column in the table
        /// </summary>
        public void GotoPreviousColumn()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectPreviousColumn));
        }
        #endregion

        #endregion

        #region SpellChecker
        /// <summary>
        /// Finds and selects the next misspelled word
        /// </summary>
        /// <returns type="bool">true: if a misspelled word was found, false otherwise</returns>
        public bool FindNextMisspelledWord()
        {
            return Convert.ToBoolean(
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.FindNextMisspelledWord),typeof(bool)),CultureInfo.CurrentCulture
                );
        }

        /// <summary>
        /// Gets the number of suggested corrections
        /// </summary>
        /// <returns>The number of spelling suggestions</returns>
        public int SpellingSuggestionsCount
        {
            get
            {
                return Convert.ToInt32(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSpellingSuggestionsCount),typeof(int)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Gets the i-th suggestion
        /// </summary>
        /// <param name="index">the suggestion index</param>
        /// <returns>the suggestion string</returns>
        public string GetSpellingSuggestion(int index)
        {
            if (index >= 0 && index < SpellingSuggestionsCount)
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSpellingSuggestion, index), typeof(string)),CultureInfo.CurrentCulture
                    );
            }
            else
            {
                throw new InvalidDataException("Index is out of expected range");
            }
        }

        /// <summary>
        /// Gets the selected misspelled word
        /// </summary>
        /// <returns>The currently selected misspelled word</returns>
        public string CurrentMisspelledWord
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetCurrentMisspelledWord),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Ignores the selected misspelling
        /// </summary>
        /// <param name="misspelled">the misspelled word to ignore</param>
        public void IgnoreMisspelledWord(string misspelled)
        {
            if (!String.IsNullOrEmpty(misspelled))
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.IgnoreMisspelledWord, misspelled));
            }
            else
            {
                throw new InvalidDataException("Misspelled word is either null or an empty string");
            }
        }

        /// <summary>
        /// Ignores all the occurences of the specified misspelled word
        /// </summary>
        /// <param name="misspelled">the word to ignore</param>
        public void IgnoreAllOfMisspelledWord(string misspelled)
        {
            if (!String.IsNullOrEmpty(misspelled))
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.IgnoreAllOfMisspelledWord, misspelled));
            }
            else
            {
                throw new InvalidDataException("Misspelled word is either null or an empty string");
            }
        }

        /// <summary>
        /// Corrects the misspelled word
        /// </summary>
        /// <param name="misspelled">the misspelled word</param>
        /// <param name="correct">correction of the misspelled word</param>
        public void CorrectMisspelledWord(string misspelled, string correct)
        {
            if (!String.IsNullOrEmpty(misspelled) && !String.IsNullOrEmpty(correct))
            {
                object[] vaIn = { misspelled, correct };
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.CorrectMisspelledWord, vaIn));
            }
            else
            {
                throw new InvalidDataException("The misspelled word and the corrected word cannot be null or empty");
            }
        }

        /// <summary>
        /// Corrects all the occurences of this misspelled word
        /// </summary>
        /// <param name="misspelled">the word to correct</param>
        /// <param name="correct">correction of the misspelled word</param>
        public void CorrectAllOfMisspelledWord(string misspelled, string correct)
        {
            if (!String.IsNullOrEmpty(misspelled) && !String.IsNullOrEmpty(correct))
            {
                object[] vaIn = { misspelled, correct };
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.CorrectAllOfMisspelledWord, vaIn));
            }
            else
            {
                throw new InvalidDataException("The misspelled word and the corrected word cannot be null or empty");
            }
        }

        /// <summary>
        /// Adds the unrecognized\misspelled word to the custom dictionary
        /// </summary>
        /// <param name="misspelled">the new word to add to the dictionary</param>
        public void AddWordToDictionary(string misspelled)
        {
            if (!String.IsNullOrEmpty(misspelled))
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.AddWordToDictionary, misspelled));
            }
            else
            {
                throw new InvalidDataException("The misspelled word is either null or an empty string");
            }
        }

        /// <summary>
        /// Deletes the selected misspelled word
        /// </summary>
        /// <param name="misspelled">the word to delete</param>
        public void DeleteMisspelledWord(string misspelled)
        {
            if (!String.IsNullOrEmpty(misspelled))
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.DeleteMisspelledWord, misspelled));
            }
            else
            {
                throw new InvalidDataException("The misspelled word is either null or an empty string");
            }
        }

        /// <summary>
        /// Sets/Gets whether or not checking should be checked as users type
        /// </summary>
        /// <param name="checkAsYouType">Flag indicating whether to turn the option on or off</param>
        public bool SpellingOptionCheckAsYouTypeOn
        {
            get
            {
                return IsCommandOn(FormControlCommandIds.CommandIds.SetSpellingOptionCheckAsYouType);
            }
            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetSpellingOptionCheckAsYouType, value));
            }
        }

        #endregion

        #region Picture Formatting

        /// <summary>
        /// Positions the picture such that it falls inline with the text
        /// </summary>
        public void SetPictureInlineWithText()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetPictureInlineWithText));
        }

        /// <summary>
        /// Positions the picture such that it falls to the left of any text
        /// </summary>
        public void SetPictureToLeftOfText()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetPictureToLeftOfText));
        }

        /// <summary>
        /// Positions the picture such that it falls to the right of any text
        /// </summary>
        public void SetPictureToRightOfText()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetPictureToRightOfText));
        }

        // <summary>
        /// Sets/Gets the height of the selected picture
        /// </summary>
        /// <returns>Height of the selected picture</returns>
        public string PictureHeight
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetPictureHeight),typeof(string)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetPictureWidth, value));
            }
        }

        /// <summary>
        /// Sets/Gets the width of the selected picture
        /// </summary>
        /// <returns>Width of the selected picture</returns>
        public string PictureWidth
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetPictureWidth),typeof(string)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetPictureWidth, value));
            }
        }

        /// <summary>
        /// Sets/Gets the alternative text of the selected picture
        /// </summary>
        /// <returns>Alternative text</returns>
        public string PictureAlternativeText
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetPictureAlternativeText),typeof(string)),CultureInfo.CurrentCulture
                    );
            }

            set
            {
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetPictureAlternativeText, value));
            }
        }

        /// <summary>
        /// Gets the alignment of the picture
        /// </summary>
        /// <returns>left,right or inline</returns>
        public string PictureAlignment
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetPictureTextWrapping),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }
        #endregion

        #region Insertion

        #region Symbol
        /// <summary>
        /// Shows the Insert a Symbol Dialog
        /// </summary>
        public void ShowInsertSymbolDialog()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowInsertSymbolDialog));
        }
        #endregion

        #region Image
        /// <summary>
        /// Inserts at image from the specified location
        /// </summary>
        /// <param name="path">path to the image</param>
        public void InsertImage(string filePath)
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertImage, filePath));
        }

        /// <summary>
        /// Inserts a Picture from a File dialog
        /// </summary>
        public void InsertPictureFromFile()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertPictureFromFile));
        }
        #endregion

        #region Horizontal Line
        /// <summary>
        /// Inserts a horizontal line into a rich text control
        /// </summary>
        public void InsertHorizontalLine()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertHorizontalLine));
        }
        #endregion

        #region Hyperlink
        /// <summary>
        /// Checks if a hyperlink is currently selected
        /// </summary>
        public bool IsHyperlinkSelected
        {
            get
            {
                return IsCommandOn(FormControlCommandIds.CommandIds.SelectHyperlink);
            }
        }

        /// <summary>
        /// Gets the URL affiliated with the hyperlink
        /// </summary>
        /// <returns></returns>
        public string HyperlinkAddress
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetHyperlinkAddress),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Gets the text affiliated with the Hyperlink
        /// </summary>
        /// <returns></returns>
        public string HyperlinkDisplayText
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetHyperlinkDisplayText),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Selects all of the current hyperlink
        /// </summary>
        public void SelectHyperlink()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SelectHyperlink));
        }

        /// <summary>
        /// Inserts a hyperlink into a control
        /// </summary>
        /// <param name="link">Where the hyperlink leads to</param>
        /// <param name="text">Text to display for the hyperlink</param>
        public void InsertHyperlink(string link, string text)
        {
            if (!String.IsNullOrEmpty(link) && !String.IsNullOrEmpty(text))
            {
                object[] vaIn = { link, text };
                ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.InsertHyperlink, vaIn));
            }
            else
            {
                throw new InvalidDataException("Both the link and the text information cannot be null or blank");
            }
        }

        /// <summary>
        /// Removes a hyperlink
        /// </summary>
        public void RemoveHyperlink()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.RemoveHyperlink));
        }
        #endregion

        #endregion

        #region Errors
        /// <summary>
        /// Selects the first error on the current view
        /// </summary>
        public void GoToFirstErrorOnView()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GotoFirstErrorOnView));
        }

        ///    <summary>
        ///    Selects the next error on the current view
        ///    </summary>
        public void GoToNextErrorOnView()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GotoNextErrorOnView));
        }

        /// <summary>
        /// Shows the message associated with the selected error
        /// </summary>
        public void ShowCurrentErrorMessage()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowCurrentErrorMessage));
        }
        #endregion

        #region Work Offline
        /// <summary>
        /// Toggles WorkOffline On/Off
        /// </summary>
        public void WorkOffline()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.WorkOffline));
        }

        #endregion

        #region Form Direction
        /// <summary>
        /// Checks if the current direction of the form is left to right
        /// </summary>
        public bool IsFormDirectionLeftToRight
        {
            get
            {
                return Convert.ToBoolean(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.IsFormDirectionLeftToRight),typeof(uint)),CultureInfo.CurrentCulture
                    );
            }
        }

        /// <summary>
        /// Checks if the current direction of the form is right to left
        /// </summary>
        public bool IsFormDirectionRightToLeft
        {
            get
            {
                return Convert.ToBoolean(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.IsFormDirectionRightToLeft),typeof(uint)),CultureInfo.CurrentCulture
                    );
            }
        }
        #endregion

        #region Text Direction
```

## C# Definition:
```cs
/// Sets the direction of the text to be the default direction
        /// </summary>
        public void SetTextDirectionDefault()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetTextDirectionDefault));
        }

        /// <summary>
        /// Sets the direction of the text to be left to right
        /// </summary>
        public void SetTextDirectionLeftToRight()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetTextDirectionLeftToRight));
        }

        /// <summary>
        /// Sets the direction of the text to be right to left
        /// </summary>
        public void SetTextDirectionRightToLeft()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetTextDirectionRightToLeft));
        }
        #endregion

        #region Submit
        /// <summary>
        /// Performs the submit action of the form
        /// </summary>
        public void Submit()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.Submit));
        }

        /// <summary>
        /// Gets the text on the InfoPath Submit Button
        /// </summary>
        public string SubmitButtonCaption
        {
            get
            {
                return Convert.ToString(
                    ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.GetSubmitButtonCaption),typeof(string)),CultureInfo.CurrentCulture
                    );
            }
        }
        #endregion

        #region Views
        /// <summary>
        /// Switches a view to the viewName
        /// </summary>
        /// <param name="viewName">name of the view</param>
        public void SwitchView(string viewName)
        {
            if (string.IsNullOrEmpty(viewName))
            {
                throw new InvalidDataException("The view name entered is either null or empty.\nPlease use a valid view.");
            }
            if (IsFormLoaded)
            {
                try
                {
                    InfoPathControl.XmlForm.ViewInfos.SwitchView(viewName);
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to switch view",ex);
                }
            }
        }

        /// <summary>
        /// Gets an array of Views within the current form template
        /// Will not return the hidded views
        /// </summary>
        /// <returns>String array of View names</returns>
        public string[] GetViews()
        {
            string[] formTemplateViews = null;

            if (IsFormLoaded)
            {
                try
                {
                    // Check the view count, only proceed if there are views
                    if (InfoPathControl.XmlForm.ViewInfos.Count > 0)
                    {
                        // instantiate the array to hold the views to return
                        formTemplateViews = new string[InfoPathControl.XmlForm.ViewInfos.Count];

                        // Cycle through the views and populate the array
                        for (int viewCounter = 0; viewCounter < InfoPathControl.XmlForm.ViewInfos.Count; viewCounter++)
                        {
                            // If the HideName property is true, then we should NOT add this to the view collection
                            // this would indicate that the solution designer did not intend for this view to be 
                            // available in the View menu.
                            if (!((ViewInfo)InfoPathControl.XmlForm.ViewInfos[viewCounter]).HideName)
                            {
                                string viewName = string.Empty;
                                viewName = InfoPathControl.XmlForm.ViewInfos[viewCounter].Name;
                                // Add the view name to the array
                                formTemplateViews[viewCounter] = viewName;
                            }
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw new HostedException("An error occurred while attempting to get the list of views", ex);
                }
            }
            return formTemplateViews;

        }
        #endregion

        #region Dialogs
        #region Borders and Shading
        /// <summary>
        /// Shows the borders and shadings dialog
        /// </summary>
        public void ShowBordersShadingDialog()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowBordersShadingDialog));
        }
        #endregion

        #region Digital Signatures
        /// <summary>
        /// Shows the Digital Signatures Dialog
        /// </summary>
        public void ShowDigitalSignaturesDialog()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowDigitalSignaturesDialog));
        }
        #endregion

        #region SetLanguage
        /// <summary>
        /// Sets the language the editor uses using the set language dialog
        /// </summary>
        public void SetLanguage()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowSetLanguageDialog));
        }

        #endregion

        #region Merge Forms
        /// <summary>
        /// Opens the Merge Forms dialog
        /// </summary>
        public void MergeForms()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowMergeFormDialog));
        }
        #endregion

        #region Import Form Data
        /// <summary>
        /// Opens the Import form data dialog
        /// </summary>
        public void ImportFormData()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowImportFormDataDialog));
        }
        #endregion

        #region Export
        /// <summary>
        /// Shows the export to web dialog
        /// </summary>
        public void ExportToWeb()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowExportToWebDialog));
        }

        /// <summary>
        /// Shows the export to PDF or XPS dialog
        /// </summary>
        public void ExportToPDFXPS()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowExportToPDFXPSDialog));
        }

        /// <summary>
        /// Shows the export to excel dialog
        /// </summary>
        public void ExportToExcel()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ShowExportToExcelDialog));
        }
        #endregion

        #endregion

        #region Asian Text Settings

        /// <summary>
        /// Sets whether spacing between asian text and numbers is on or off
        /// </summary>
        public void SetAutoSpaceBetweenAsianTextAndNumbers()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetAutoSpaceBetweenAsianTextAndNumbers));
        }

        /// <summary>
        /// Set whether spacing between asian text and latin text is on or off
        /// </summary>
        public void SetAutoSpaceBetweenAsianAndLatinText()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.SetAutoSpaceBetweenAsianAndLatinText));
        }

        /// <summary>
        /// Turns of all spacing adjustments for asian text
        /// </summary>
        public void ClearAutoSpace()
        {
            ChkResult(ExecuteCommand(FormControlCommandIds.CommandIds.ClearAutoSpace));
        }

        #endregion

        #region Is Form Loaded
        /// <summary>
        /// Checks whether or not a document is loaded
        /// </summary>
        /// <returns>true if a document is loaded, otherwise false</returns>
        public bool IsFormLoaded
        {
            get
            {
                if (InfoPathControl.XmlForm == null)
                {
                    return false;
                }
                else
                {
                    return true;
                }
            }
        }
        #endregion
    }
```
