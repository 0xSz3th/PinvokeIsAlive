
## C# Signature:
```cs
[DllImport("comctl32.dll", SetLastError=true)]
static extern HRESULT TaskDialogIndirect
(
     in TASKDIALOGCONFIG pTaskConfig,
     out int pnButton,
     out int pnRadioButton,
     [MarshalAs( UnmanagedType.Bool ), Out] out bool pfverificationFlagChecked
);
```

## C# Signature:
```cs
[DllImport("comctl32.dll", CharSet = CharSet.Unicode, PreserveSig = true)]
    public static extern IntPtr TaskDialogIndirect
       [In] ref TASKDIALOGCONFIG pTaskConfig, 
       out int pnButton,
       out int pnRadioButton,
       [MarshalAs(UnmanagedType.Bool)] out bool pfVerificationFlagChecked
        );
```

## Task Dialog config structure c#
```cs
/// <summary>The Task Dialog config structure.</summary>
    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode, Pack = 1)]
    public struct TaskDialogConfig
    {
        public uint cbSize;
        public IntPtr hwndParent;
        public IntPtr hInstance;
        public TaskDialogFlags dwFlags;
        public TaskDialogButton dwCommonButtons;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pszWindowTitle;
        public IntPtr hMainIcon;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pszMainInstruction;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pszContent;
        public uint cButtons;
        public IntPtr pButtons;
        public int nDefaultButton;
        public uint cRadioButtons;
        public IntPtr pRadioButtons;
        public int nDefaultRadioButton;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pszVerificationText;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pszExpandedInformation;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pszExpandedControlText;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pszCollapsedControlText;
        public IntPtr hFooterIcon;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string pszFooter;
        public TaskDialogCallback pfCallback;
        public IntPtr lpCallbackData;
        public uint cxWidth;
    }
```

## Notes
```cs
<dependentAssembly>
      <assemblyIdentity
      type="win32"
      name="Microsoft.Windows.Common-Controls"
      version="6.0.0.0"
      processorArchitecture="*"
      publicKeyToken="6595b64144ccf1df"
      language="*"
    />
    </dependentAssembly>
```

## VB Signature:
```cs
Declare Function TaskDialogIndirect Lib "comctl32.dll" (TODO) As TODO

<DllImport("comctl32.dll", SetLastError := True)> _
Private Shared Function TaskDialogIndirect(<[In]> pTaskConfig As TASKDIALOGCONFIG, <Out> ByRef pnButton As Integer, <Out> ByRef pnRadioButton As Integer, <MarshalAs(UnmanagedType.Bool), Out> ByRef pfverificationFlagChecked As Boolean) As HRESULT
End Function
```

## Sample Code:
```cs
/// <summary>The TaskDialogIndirect function creates, displays, and operates a task dialog. The task dialog contains application-defined icons, messages, title, verification check box, command links, push buttons, and radio buttons. This function can register a callback function to receive notification messages.</summary>
    /// <param name="taskConfig">A pointer to a <see cref="TaskDialogConfig"/> structure that contains information used to display the task dialog.</param>
    /// <param name="button">Address of a variable that receives one of the button IDs specified in the <paramref name="button"/> member of the <paramref name="taskConfig"/> parameter. If this parameter is <see langword="null"/>, no value is returned.</param>
    /// <param name="radioButton">Address of a variable that receives one of the button IDs specified in the <paramref name="radioButton"/> member of the <paramref name="taskConfig"/> parameter. If this parameter is <see langword="null"/>, no value is returned.</param>
    /// <param name="verificationFlagChecked"><see langword="true"/> if the verification <see cref="CheckBox"/> was checked when the dialog was dismissed; otherwise, false</param>
    /// <returns>The result</returns>
    [DllImport(@"comctl32.dll", CharSet = CharSet.Unicode, PreserveSig = false)]
    internal static extern Result TaskDialogIndirect([In] TaskDialogConfig taskConfig, [Out] out int button, [Out] out int radioButton, [MarshalAs(UnmanagedType.Bool), Out] out bool verificationFlagChecked);
```
