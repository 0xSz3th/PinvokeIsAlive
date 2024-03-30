
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr LoadCursor(IntPtr hInstance, int lpCursorName);
```

## VB Signature:
```cs
<DllImport("user32.dll", CharSet:=CharSet.Auto)> _
Public Shared Function LoadCursor( _
    ByVal hInstance As IntPtr, _
    ByVal lpCursorName As String) As IntPtr
End Function
```

## Common VB Overloads:
```cs
<DllImport("user32.dll", CharSet:=CharSet.Auto)> _
Public Shared Function LoadCursor( _
    ByVal hInstance As IntPtr, _
    ByVal lpCursorName As Integer) As IntPtr
End Function
```

## C# Sample Code:
```cs
IntPtr handle = LoadCursor(IntPtr.Zero, IDC_Arrow);
```

## VB Sample Code:
```cs
Dim HighlightPointer as Cursor = ColorCursor.LoadCursor(101)    

   ''' <summary>
   '''   Provides ability to load color and/or animated cursor for the form or control. 
   '''   Note: cursor must be embedded as native win32 resource in the assembly.
   ''' </summary>
   Private Class ColorCursor

      Private Declare Function LoadCursorAPI Lib "user32.dll" Alias "LoadCursorA" (ByVal hInstance As IntPtr, ByVal lpCursorName As String) As IntPtr

      Public Shared Function LoadCursor(ByVal embededWin32ResourceID As Integer) As Cursor
     Dim cursor As Cursor = TryLoadCursor(embededWin32ResourceID)
     If cursor Is Nothing Then
        Throw New System.ComponentModel.Win32Exception(Err.LastDllError)
     Else
        Return cursor
     End If
      End Function

      Public Shared Function TryLoadCursor(ByVal embededWin32ResourceID As Integer) As Cursor
     Dim hInstance As IntPtr = System.Runtime.InteropServices.Marshal.GetHINSTANCE(System.Reflection.Assembly.GetExecutingAssembly.GetModules()(0))
     Dim cPtr As IntPtr = LoadCursorAPI(hInstance, embededWin32ResourceID)
     cPtr = LoadCursorAPI(hInstance, "#" & embededWin32ResourceID)
     If cPtr = IntPtr.Zero Then
        Return Nothing
     Else
        Return New Cursor(cPtr)
     End If
      End Function

   End Class
```

## How to Embed Multiple Icons and Color/Animated Cursors in VS2010 VB project as Native Win32 Resources:
```cs
1. Open your EXE or DLL in Visual Studio (either File->Open File or just drag and drop it into IDE).
2. Add icons and/or cursors to the EXE or DLL
3. Save file.
```

## How to Embed Multiple Icons and Color/Animated Cursors in VS2010 VB project as Native Win32 Resources:
```cs
1. Find native win32 resource file (*.res) on the web. Google “Embedding Multiple Icons into .NET Executables” and download the sample project which contains *.res file. VS2010 does not have the template to create this file; however the editor is still there.

2. Rename file to assemblyWin32.res, include it in your project, and compile it as content in Build Action.

3. Add icons and/or cursors to the assemblyWin32.res file.

4. Open your project file in notepad (*.vbProj) and add the following block: 

      <PropertyGroup> 
     <Win32Resource>assemblyWin32.res</Win32Resource> 
      </PropertyGroup>

    You can put it after condition block. Here is the example:

      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|x86' ">
    ...
    ...
      </PropertyGroup>

5. If you have included icons in the Win32 resource file for your EXE then remove application icon in project properties->Application Tab (this icon will no longer be used).

6. Build the project
```
