
## C# Signature:
```cs
[DllImport("shell32.dll", CharSet=CharSet.Auto)]
static extern uint ExtractIconEx(string szFileName, int nIconIndex,
   IntPtr[] phiconLarge, IntPtr[] phiconSmall, uint nIcons);
```

## VB Signature:
```cs
<DllImport("shell32.dll", CharSet:=CharSet.Auto)> _
Shared Function ExtractIconEx(ByVal szFileName As String, _
            ByVal nIconIndex As Integer, _
            ByRef phiconLarge() As IntPtr, _
            ByRef phiconSmall() As IntPtr, _
            ByVal nIcons As UInteger) As UInteger
End Function
```

## VB 6 Signature:
```cs
Declare Function ExtractIconEx _
     Lib "shell32.dll" _
     Alias "ExtractIconExA" _
        (ByVal lpszFile As String, _
         ByVal nIconIndex As Integer, _
         ByRef phiconLarge As Integer, _
         ByRef phiconSmall As Integer, _
         ByVal nIcons As Long) As Integer
```

## Sample Code:
```cs
namespace Martin.Hyldahl.Examples.ExtractIconEx
{
    /* 
     * Example using ExtractIconEx
     * Created by Martin Hyldahl (alanadin@post8.tele.dk)
     * http://www.hyldahlnet.dk
     */

    using System;
    using System.Drawing;
    using System.Runtime.InteropServices;

    /// <summary>
    /// Example using ExtractIconEx
    /// </summary>
    public class ExtractIconExample
    {
    /* CONSTRUCTORS */
    static ExtractIconExample()
    {
    }

    // HIDE INSTANCE CONSTRUCTOR
    private ExtractIconExample()
    {
    }

    [DllImport("Shell32", CharSet=CharSet.Auto)]
    private static unsafe extern int ExtractIconEx (
        string lpszFile,
        int nIconIndex,
        IntPtr[] phIconLarge, 
        IntPtr[] phIconSmall,
        int nIcons);

    [DllImport("user32.dll", EntryPoint="DestroyIcon", SetLastError=true)]
    private static unsafe extern int DestroyIcon(IntPtr hIcon);

    public static Icon ExtractIconFromExe(string file, bool large)
    {
        unsafe
        {
        int readIconCount = 0;
        IntPtr[] hDummy  = new IntPtr[1] {IntPtr.Zero};
        IntPtr[] hIconEx = new IntPtr[1] {IntPtr.Zero};

        try
        {
            if(large)
            readIconCount = ExtractIconEx(file,0, hIconEx, hDummy, 1);
            else
            readIconCount = ExtractIconEx(file,0, hDummy, hIconEx, 1);

            if(readIconCount > 0 && hIconEx[0] != IntPtr.Zero)
            {
            // GET FIRST EXTRACTED ICON
            Icon extractedIcon = (Icon)Icon.FromHandle(hIconEx[0]).Clone();

            return extractedIcon;
            }
            else // NO ICONS READ
            return null;
        }
        catch(Exception ex)
        {
            /* EXTRACT ICON ERROR */

            // BUBBLE UP
            throw new ApplicationException("Could not extract icon", ex);
        }
        finally
        {
            // RELEASE RESOURCES
            foreach(IntPtr ptr in hIconEx)
            if(ptr != IntPtr.Zero)
                DestroyIcon(ptr);

            foreach(IntPtr ptr in hDummy)
            if(ptr != IntPtr.Zero)
                DestroyIcon(ptr);
        }
        }
    }
    }
}
```

## Sample Code (VB Version of above):
```cs
Imports System.Runtime.InteropServices
Imports System.Drawing

Module IconExtract
    <DllImport("shell32.dll", CharSet:=CharSet.Auto)> _
    Function ExtractIconEx(ByVal szFileName As String, _
        ByVal nIconIndex As Integer, _
        ByVal phiconLarge() As IntPtr, _
        ByVal phiconSmall() As IntPtr, _
        ByVal nIcons As Integer) As Integer
    End Function
    <DllImport("user32.dll", EntryPoint:="DestroyIcon", SetLastError:=True)> _
    Function DestroyIcon(ByVal hIcon As IntPtr) As Integer
    End Function

    Public Function WriteIconOut(ByVal iconsrcpath As String, ByVal icondestpath As String)
    Dim iconsrc As Icon = ExtractIconFromExe(iconsrcpath, True)
    iconsrc.Save(System.IO.File.OpenWrite(icondestpath))
    End Function

    Public Function ExtractIconFromExe(ByVal f As String, ByVal large As Boolean) As Icon
    Dim readIconCount As Integer = 0
    Dim hDummy As IntPtr() = New IntPtr(0) {IntPtr.Zero}
    Dim hIconEx As IntPtr() = New IntPtr(0) {IntPtr.Zero}

    Try
        If (large) Then
        readIconCount = ExtractIconEx(f, 0, hIconEx, hDummy, 1)
        Else
        readIconCount = ExtractIconEx(f, 0, hDummy, hIconEx, 1)
        End If

        If (readIconCount > 0 AndAlso Not hIconEx(0).Equals(IntPtr.Zero)) Then
        ' GET FIRST EXTRACTED ICON
        Dim extractedIcon As Icon = Icon.FromHandle(hIconEx(0)).Clone()
        Return extractedIcon
        Else ' NO ICONS READ
        Return Nothing
        End If
    Catch ex As Exception
        ' EXTRACT ICON ERROR 
        ' BUBBLE UP
        Throw New ApplicationException("Could not extract icon", ex)
    Finally
        'RELEASE RESOURCES
        For Each ptr As IntPtr In hIconEx
        If (Not ptr.Equals(IntPtr.Zero)) Then
            DestroyIcon(ptr)
        End If
        Next ptr

        For Each ptr As IntPtr In hDummy
        If Not (ptr.Equals(IntPtr.Zero)) Then
            DestroyIcon(ptr)
        End If
        Next ptr
    End Try
    End Function
End Module
```
