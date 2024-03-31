
## C# Definition:
```cs
using System.Runtime.InteropServices;
    using System;
    using System.Text;
    public enum UrlZone
    {
    LocalMachine,
    Intranet,
    Trusted,
    Internet,
    Untrusted
    }

    public enum UrlAction
    {
    ActiveXScriptletRun = unchecked((int)0x00001209),
    DownloadUnsignedActiveX = unchecked((int)0x00001004)
    }

    public enum UrlZoneReg
    {
    Default,
    LocalMachineKey,
    CurrentUserKey
    }

    public enum URLTEMPLATE  
    { 
    URLTEMPLATE_CUSTOM      = 0x00000,
    URLTEMPLATE_PREDEFINED_MIN  = 0x10000,
    URLTEMPLATE_LOW         = 0x10000,
    URLTEMPLATE_MEDLOW      = 0x10500,
    URLTEMPLATE_MEDIUM      = 0x11000,
    URLTEMPLATE_MEDHIGH     = 0x11500,
    URLTEMPLATE_HIGH        = 0x12000,
    URLTEMPLATE_PREDEFINED_MAX  = 0x20000
    } 

    [StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    public struct ZoneAttributes
    {
    public uint Size;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 260)]
    public string DisplayName;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 200)]
    public string Description;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 260)]
    public string IconPath;
    public uint TemplateMinLevel;
    public uint TemplateRecommended;
    public uint TemplateCurrentLevel;
    public uint Flags;
    };





    [ComImport,
     Guid("79eac9ef-baf9-11ce-8c82-00aa004ba90b"),
     InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IInternetZoneManager
    {
    [PreserveSig]
    int GetZoneAttributes(uint dwZone,
                  ref ZoneAttributes pZoneAttributes);

    [PreserveSig]
    int SetZoneAttributes(uint dwZone,
                  ref ZoneAttributes pZoneAttributes);

    [PreserveSig]
    int GetZoneCustomPolicy(uint dwZone,
                ref Guid guidKey,
                out IntPtr ppPolicy,
                ref uint pcbPolicy,
                uint urlZoneReg);

    [PreserveSig]
    int SetZoneCustomPolicy(uint dwZone,
                ref Guid guidKey,
                IntPtr pPolicy,
                uint cbPolicy,
                uint urlZoneReg);

    [PreserveSig]
    int GetZoneActionPolicy(uint dwZone,
                uint dwAction,
                IntPtr pPolicy,
                uint cbPolicy,
                uint urlZoneReg);

    [PreserveSig]
    int SetZoneActionPolicy(uint dwZone,
                uint dwAction,
                IntPtr pPolicy,
                uint cbPolicy,
                uint urlZoneReg);

    [PreserveSig]
    int PromptAction(uint dwAction,
             HandleRef hwndParent,
             StringBuilder pwszUrl,
             StringBuilder pwszText,
             uint dwPromptFlags);

    [PreserveSig]
    int LogAction(uint dwAction,
              StringBuilder pwszUrl,
              StringBuilder pwszText,
              uint dwLogFlags);

    [PreserveSig]
    int CreateZoneEnumerator(ref uint pdwEnum,
                 ref uint pdwCount,
                 uint dwFlags);

    [PreserveSig]
    int GetZoneAt(uint dwEnum,
              uint dwIndex,
              ref uint pdwZone);

    [PreserveSig]
    int DestroyZoneEnumerator(uint dwEnum);

    [PreserveSig]
    int CopyTemplatePoliciesToZone(uint dwTemplate,
                       uint dwZone,
                       uint dwReserved);
    }



    public sealed class InternetZoneManager : IDisposable
    {
    private IInternetZoneManager izm;

    public InternetZoneManager()
    {
        this.izm = Activator.CreateInstance(Type.GetTypeFromCLSID(new Guid("7b8a2d95-0ac9-11d1-896c-00c04Fb6bfc4"))) as IInternetZoneManager;
    }

    public ZoneAttributes GetZoneAttributes(UrlZone zone)
    {
        ZoneAttributes za = new ZoneAttributes();

        if (this.izm.GetZoneAttributes((uint)zone, ref za) == 0)
        {
        return za;
        }

        throw new Exception();
    }

    public void SetZoneAttributes(UrlZone zone, ZoneAttributes attributes)
    {
        attributes.Size = (uint)Marshal.SizeOf(attributes);

        if (this.izm.SetZoneAttributes((uint)zone, ref attributes) != 0)
        {
        throw new Exception();
        }
    }

    public byte[] GetZoneActionPolicy(UrlZone zone, UrlAction action, UrlZoneReg zoneReg)
    {
        IntPtr pPolicy = Marshal.AllocHGlobal(8196);

        try
        {
        if (this.izm.GetZoneActionPolicy((uint)zone, (uint)action, pPolicy, 8196, (uint)zoneReg) == 0)
        {
            byte[] buff = new byte[8196];

            for (int i = 0; i < buff.Length; i++)
            {
            buff[i] = Marshal.ReadByte(pPolicy, i);
            }

            return buff;
        }

        throw new Exception();
        }
        finally
        {
        Marshal.FreeHGlobal(pPolicy);
        }
    }

    public int CopyTemplatePoliciesToZone(URLTEMPLATE template, UrlZone zone)
    {
        try
        {
        if (this.izm.CopyTemplatePoliciesToZone((uint)template, (uint)zone, 0) == 0)
        {
            return 0;
        }
        throw new Exception();
        }
        finally { }
    }

    public void Dispose()
    {
        if (this.izm != null)
        {
        Marshal.ReleaseComObject(this.izm);
        this.izm = null;
        }

        GC.SuppressFinalize(this);
    }
    }
```

## VB Definition:
```cs
Imports System.Runtime.InteropServices

    Public Enum UrlZone
    LocalMachine
    Intranet
    Trusted
    Internet
    Untrusted
    End Enum

    Public Enum UrlAction
    ActiveXScriptletRun = 4617
    DownloadUnsignedActiveX = 4100
    End Enum

    Public Enum UrlZoneReg
    [Default]
    LocalMachineKey
    CurrentUserKey
    End Enum

    Public Enum UrlTemplate
    Custom
    Low = &H10000
    MediumLow = &H10500
    Medium = &H11000
    MediumHigh = &H11500
    High = &H12000
    End Enum

    <StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Unicode)> _
    Public Structure ZoneAttributes
    Public Size As UInteger
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=260)> Public DizplayName As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=200)> Public Description As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=260)> Public IconPath As String
    Public TemplateMinLevel As UInteger
    Public TemplateRecommended As UInteger
    Public TemplateCurrentLevel As UInteger
    Public Flags As UInteger
    End Structure


    <Guid("79eac9ef-baf9-11ce-8c82-00aa004ba90b")> _
    <ComImport()> _
    <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
    Public Interface IInternetZoneManager
    <PreserveSig()> _
    Function GetZoneAttributes(ByVal dwZone As UInteger,
                  ByRef pZoneAttributes As ZoneAttributes) As Integer

    <PreserveSig()> _
    Function SetZoneAttributes(ByVal dwZone As UInteger,
                  ByRef pZoneAttributes As ZoneAttributes) As Integer

    <PreserveSig()> _
    Function GetZoneCustomPolicy(ByVal dwZone As UInteger,
                <[In]()> ByRef guidKey As Guid,
                ByRef ppPolicy As IntPtr,
                ByRef pcbPolicy As UInteger,
                ByVal urlZoneReg As UrlZoneReg) As Integer

    <PreserveSig()> _
    Function SetZoneCustomPolicy(ByVal dwZone As UInteger,
                <[In]()> ByRef guidKey As Guid,
                ByVal pPolicy As IntPtr,
                ByVal pcbPolicy As UInteger,
                ByVal urlZoneReg As UrlZoneReg) As Integer

    <PreserveSig()> _
    Function GetZoneActionPolicy(ByVal dwZone As UInteger,
                ByVal dwAction As UInteger,
                ByVal pPolicy As IntPtr,
                ByVal cbPolicy As UInteger,
                ByVal urlZoneReg As UrlZoneReg) As Integer

    <PreserveSig()> _
    Function SetZoneActionPolicy(ByVal dwZone As UInteger,
                ByVal dwAction As UInteger,
                ByVal pPolicy As IntPtr,
                ByVal cbPolicy As UInteger,
                ByVal urlZoneReg As UrlZoneReg) As Integer

    <PreserveSig()> _
    Function PromptAction(ByVal dwAction As UInteger,
             ByVal hwndParent As IntPtr,
             <MarshalAs(UnmanagedType.LPWStr)> ByVal pwszUrl As String,
             <MarshalAs(UnmanagedType.LPWStr)> ByVal pwszText As String,
             ByVal dwPromptFlags As UInteger) As Integer

    <PreserveSig()> _
    Function LogAction(ByVal dwAction As UInteger,
              <MarshalAs(UnmanagedType.LPWStr)> ByVal pwszUrl As String,
              <MarshalAs(UnmanagedType.LPWStr)> ByVal pwszText As String,
              ByVal dwLogFlags As UInteger) As Integer

    <PreserveSig()> _
    Function CreateZoneEnumerator(ByRef pdwEnum As UInteger,
                 ByRef pdwCount As UInteger,
                 ByVal dwFlags As UInteger) As Integer

    <PreserveSig()> _
    Function GetZoneAt(ByVal dwEnum As UInteger,
              ByVal dwIndex As UInteger,
              ByRef pdwZone As UInteger) As Integer

    <PreserveSig()> _
    Function DestroyZoneEnumerator(ByVal dwEnum As UInteger) As Integer

    <PreserveSig()> _
    Function CopyTemplatePoliciesToZone(ByVal dwTemplate As UInteger,
                       ByVal dwZone As UInteger,
                       ByVal dwReserved As UInteger) As Integer
    End Interface


    Public NotInheritable Class InternetZoneManager
    Implements IDisposable

    Private izm As IInternetZoneManager

    Public Sub New()
        MyBase.New()
        Me.izm = CType(Activator.CreateInstance(Type.GetTypeFromCLSID(New Guid("7b8a2d95-0ac9-11d1-896c-00c04Fb6bfc4"))), IInternetZoneManager)
    End Sub

    Public Function GetZoneAttributes(ByVal zone As UrlZone) As ZoneAttributes
        Dim za As ZoneAttributes = New ZoneAttributes
        If (Me.izm.GetZoneAttributes(CType(zone, UInteger), za) = 0) Then
        Return za
        End If
        Throw New Exception
    End Function

    Public Sub SetZoneAttributes(ByVal zone As UrlZone, ByVal attributes As ZoneAttributes)
        attributes.Size = CType(Marshal.SizeOf(attributes), UInteger)
        If (Me.izm.SetZoneAttributes(CType(zone, UInteger), attributes) <> 0) Then
        Throw New Exception
        End If
    End Sub

    Public Function GetZoneActionPolicy(ByVal zone As UrlZone, ByVal action As UrlAction, ByVal zoneReg As UrlZoneReg) As Byte()
        Dim pPolicy As IntPtr = Marshal.AllocHGlobal(8196)
        Try
        If (Me.izm.GetZoneActionPolicy(CType(zone, UInteger), CType(action, UInteger), pPolicy, 8196, CType(zoneReg, UInteger)) = 0) Then
            Dim buff() As Byte = New Byte((8196) - 1) {}
            Dim i As Integer = 0
            Do While (i < buff.Length)
            buff(i) = Marshal.ReadByte(pPolicy, i)
            i = (i + 1)
            Loop
            Return buff
        End If
        Throw New Exception
        Finally
        Marshal.FreeHGlobal(pPolicy)
        End Try
    End Function

    Public Function CopyTemplatePoliciesToZone(ByVal template As UrlTemplate, ByVal zone As UrlZone) As Integer
        If (Me.izm.CopyTemplatePoliciesToZone(CType(template, UInteger), CType(zone, UInteger), 0) = 0) Then
        Return 0
        End If
        Throw New Exception
    End Function

    Public Sub Dispose() Implements IDisposable.Dispose
        If (Not (Me.izm) Is Nothing) Then
        Marshal.ReleaseComObject(Me.izm)
        Me.izm = Nothing
        End If
        GC.SuppressFinalize(Me)
    End Sub

    End Class
```
