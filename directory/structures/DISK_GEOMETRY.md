
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct DISK_GEOMETRY
{
   public long Cylinders;
   public MEDIA_TYPE MediaType;
   public int TracksPerCylinder;
   public int SectorsPerTrack;
   public int BytesPerSector;

   public long DiskSize
   {
     get
     {
       return Cylinders * (long)TracksPerCylinder * (long)SectorsPerTrack * (long)BytesPerSector;
     }
   }
}
```

## VB 2008
```cs
<System.Runtime.InteropServices.StructLayout(LayoutKind.Sequential)> _
Public Structure DISK_GEOMETRY
    Public Cylinders As Long
    Public MediaType As MEDIA_TYPE
    Public TracksPerCylinder As Integer
    Public SectorsPerTrack As Integer
    Public BytesPerSector As Integer

    Public ReadOnly Property disksize() As Long
    Get
        return Cylinders * CLng(TracksPerCylinder) * CLng(SectorsPerTrack) * CLng(BytesPerSector;)
    End Get
    End Property
End Structure
```
