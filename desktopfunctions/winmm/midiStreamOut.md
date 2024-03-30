
## C# Signature:
```cs
[DllImport("winmm.dll")]
static extern Int32 midiStreamOut(IntPtr hMidiStream, MIDIHDR lpMidiHdr, uint cbMidiHdr);
```

## VB Signature:
```cs
Declare Function midiStreamOut Lib "winmm.dll" (ByVal hMidiStream As IntPtr, ByVal lpMidiHdr As MIDIHDR, ByVal cbMidiHdr As UInteger) As Integer
```

## C# User-Defined Types:
```cs
struct MIDIHDR
{
     string lpdata;
     int dwBufferLength;
     int dwBytesRecorded;
     IntPtr dwUser;
     int dwFlags;
     MIDIHDR lpNext;
     IntPtr reserved;
     int dwOffset;
     IntPtr dwReserved;
}
```

## VB User-Defined Types:
```cs
Structure MIDIHDR
     Dim lpData As String
     Dim dwBufferLength As Integer
     Dim dwBytesRecorded As Integer
     Dim dwUser As IntPtr
     Dim dwFlags As Integer
     Dim lpNext As Object
     Dim reserved As IntPtr
     Dim dwOffset As Integer
     Dim dwReserved As IntPtr
End Structure
```
