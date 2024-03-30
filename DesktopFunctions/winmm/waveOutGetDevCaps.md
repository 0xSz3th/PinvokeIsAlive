
## C# Signature:
```cs
[DllImport("winmm.dll", SetLastError = true, CharSet = CharSet.Auto)]
public static extern uint waveOutGetDevCaps(IntPtr hwo,ref WAVEOUTCAPS pwoc,uint cbwoc);
```

## VB Signature:
```cs
Declare Auto Function waveOutGetDevCaps Lib "winmm.dll" (ByVal uDeviceID as Integer, ByRef lpCaps As WAVEOUTCAPS, _
ByVal uSize As Integer) As Integer
```

## Constants Used:
```cs
Public Const C_MAXPNAMELEN As Integer = 32
Public Const WAVE_MAPPER As Integer = -1    'Specifies default device ID
```

## Structures Used:
```cs
VB.NET 2005 - Use the following structure: WAVEOUTCAPS

<Runtime.InteropServices.StructLayout(Runtime.InteropServices.LayoutKind.Sequential, CharSet:=Runtime.InteropServices.CharSet.Auto)> _
Public Structure WAVEOUTCAPS
     Public wMid As Short
     Public wPid As Short
     Public vDriverVersion As Integer

     <System.Runtime.InteropServices.MarshalAs(System.Runtime.InteropServices.UnmanagedType.ByValTStr, SizeConst:=32)> _
     Public szPname As String

     Public dwFormats As Integer
     Public wChannels As Short
     Public wReserved As Short
     Public dwSupport As Integer
End Structure

C# 2005 version of structure
[System.Runtime.InteropServices.StructLayout(Runtime.InteropServices.LayoutKind.Sequential, CharSet = System.Runtime.InteropServices.CharSet.Auto)]
public struct WAVEOUTCAPS
{
     public short wMid;
     public short wPid;
     public int vDriverVersion;

     [MarshalAs(System.Runtime.InteropServices.UnmanagedType.ByValTStr, SizeConst = 32)]
     public string szPname;

     public int dwFormats;
     public short wChannels;
     public short wReserved;
     public int dwSupport;
}
```

## Sample Code:
```cs
Sub ShowDeviceCaps()
     Dim i As Integer
     Dim wc As New WAVEOUTCAPS

     MsgBox("Number of Wave Devices: " & waveOutGetNumDevs(), , "WAVE DEVICES")

     For i = 0 To waveOutGetNumDevs() - 1
         ' waveOutGetDevCaps(i, wc, Len(wc))
         waveOutGetDevCaps(i, wc, System.Runtime.InteropServices.Marshal.SizeOf(wc))   
         MsgBox("MID = " & wc.wMid & Chr(13) & "PID = " & wc.wPid & Chr(13) & "Version = " & _
         wc.vDriverVersion & Chr(13) & "Name = " & wc.szPname & Chr(13) & "Formats = " & wc.dwFormats & _
         Chr(13) & "Channels = " & wc.wChannels, , "Device ID = " & i + 1)
     Next i
End Sub
```

##  C# Code
```cs
/// <summary>
    /// 
    /// </summary>
    [StructLayout(LayoutKind.Sequential, Pack = 4, CharSet = CharSet.Auto)]
    public struct WAVEOUTCAPS
    {
        public short wMid;
        public short wPid;
        public int vDriverVersion;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
        private string szPname;
        public uint dwFormats;
        public short wChannels;
        public short wReserved;
        public uint dwSupport;

        public override string ToString()
        {
        return string.Format("wMid:{0}|wPid:{1}|vDriverVersion:{2}|'szPname:{3}'|dwFormats:{4}|wChannels:{5}|wReserved:{6}|dwSupport:{7}", new object[] { wMid, wPid, vDriverVersion, szPname, dwFormats, wChannels, wReserved, dwSupport });
        }
    }

    /// <summary>
    /// 
    /// </summary>
    [StructLayout(LayoutKind.Sequential, Pack = 4, CharSet = CharSet.Auto)]
    public struct WAVEINCAPS
    {
        public short wMid;
        public short wPid;
        public int vDriverVersion;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 32)]
        public string szPname;
        public uint dwFormats;
        public short wChannels;
        public short wReserved;
        //public int dwSupport;

        public override string ToString()
        {
        return string.Format("wMid:{0}|wPid:{1}|vDriverVersion:{2}|'szPname:{3}'|dwFormats:{4}|wChannels:{5}|wReserved:{6}", new object[] { wMid, wPid, vDriverVersion, szPname, dwFormats, wChannels, wReserved });
        }
    }

    public static WAVEOUTCAPS[] GetDevCapsPlayback()
    {
        uint waveOutDevicesCount = waveOutGetNumDevs();
        if (waveOutDevicesCount > 0)
        {
        WAVEOUTCAPS[] list = new WAVEOUTCAPS[waveOutDevicesCount];
        for (int uDeviceID = 0; uDeviceID < waveOutDevicesCount; uDeviceID++)
        {
            WAVEOUTCAPS waveOutCaps = new WAVEOUTCAPS();
            waveOutGetDevCaps(uDeviceID, ref waveOutCaps, Marshal.SizeOf(typeof(WAVEOUTCAPS)));
            System.Diagnostics.Debug.WriteLine("\n" + waveOutCaps.ToString());
            list[uDeviceID] = waveOutCaps;
        }
        return list;
        }
        else
        {
        return null;
        }
    }

    public static WAVEINCAPS[] GetDevCapsRecording()
    {
        uint waveInDevicesCount = waveInGetNumDevs();
        if (waveInDevicesCount > 0)
        {
        WAVEINCAPS[] list = new WAVEINCAPS[waveInDevicesCount];
        for (int uDeviceID = 0; uDeviceID < waveInDevicesCount; uDeviceID++)
        {
            WAVEINCAPS waveInCaps = new WAVEINCAPS();
            waveInGetDevCaps(uDeviceID, ref waveInCaps, Marshal.SizeOf(typeof(WAVEINCAPS)));
            System.Diagnostics.Debug.WriteLine("\n" + waveInCaps.ToString());
            list[uDeviceID] = waveInCaps;
        }
        return list;
        }
        else
        {
        return null;
        }
    }

    [DllImport("winmm.dll", SetLastError = true, CharSet = CharSet.Auto)]
    public static extern uint waveInGetDevCaps(int hwo, ref WAVEINCAPS pwic, /*uint*/ int cbwic);

    [DllImport("winmm.dll", SetLastError = true)]
    public static extern uint waveInGetNumDevs();

    [DllImport("winmm.dll", SetLastError = true, CharSet = CharSet.Auto)]
    public static extern uint waveOutGetDevCaps(int hwo, ref WAVEOUTCAPS pwoc, /*uint*/ int cbwoc);

    [DllImport("winmm.dll", SetLastError = true)]
    static extern uint waveOutGetNumDevs();
    }
```
