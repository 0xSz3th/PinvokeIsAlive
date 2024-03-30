
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr CreatePopupMenu();
```

## Sample Code:
```cs
[Guid("6B3A1F0C-C382-40d6-AA13-33B0AB46EEAA")]
    public class BatchResultContextMenu: IShellExtInit, IContextMenu
    {
        #region Protected Members
        protected const string guid = "{6B3A1F0C-C382-40d6-AA13-33B0AB46EEAA}";
        protected string m_fileName;
        protected uint m_hDrop = 0;
        #endregion

        #region IContextMenu
        // IContextMenu
        int    IContextMenu.QueryContextMenu(uint hMenu, uint iMenu, int idCmdFirst, int idCmdLast, uint uFlags)
        {
            // Create the popup to insert
            uint hmnuPopup = Helpers.CreatePopupMenu();

            int id = 1;
            if ( (uFlags & 0xf) == 0 || (uFlags & (uint)CMF.CMF_EXPLORE) != 0)
            {
                uint nselected = Helpers.DragQueryFile(m_hDrop, 0xffffffff, null, 0);
                if (nselected == 1)
                {
                    StringBuilder sb = new StringBuilder(1024);
                    Helpers.DragQueryFile(m_hDrop, 0, sb, sb.Capacity + 1);
                    m_fileName = sb.ToString();

                    // Populate the popup menu with file-specific items
                    id = PopulateMenu(hmnuPopup, idCmdFirst+ id);
                }

                // Add the popup to the context menu
                MENUITEMINFO mii = new MENUITEMINFO();
                mii.cbSize = 48;
                mii.fMask = (uint) MIIM.TYPE | (uint)MIIM.STATE | (uint) MIIM.SUBMENU;
                mii.hSubMenu = (int) hmnuPopup;
                mii.fType = (uint) MF.STRING;
                mii.dwTypeData = "Actions";
                mii.fState = (uint) MF.ENABLED;
                Helpers.InsertMenuItem(hMenu, (uint)iMenu, 1, ref mii);

                // Add a separator
                MENUITEMINFO sep = new MENUITEMINFO();
                sep.cbSize = 48;
                sep.fMask = (uint )MIIM.TYPE;
                sep.fType = (uint) MF.SEPARATOR;
                Helpers.InsertMenuItem(hMenu, iMenu+1, 1, ref sep);

            }
            return id;
        }

        void AddMenuItem(uint hMenu, string text, int id, uint position)
        {
            MENUITEMINFO mii = new MENUITEMINFO();
            mii.cbSize = 48;
            mii.fMask = (uint)MIIM.ID | (uint)MIIM.TYPE | (uint)MIIM.STATE;
            mii.wID    = id;
            mii.fType = (uint)MF.STRING;
            mii.dwTypeData    = text;
            mii.fState = (uint)MF.ENABLED;
            Helpers.InsertMenuItem(hMenu, position, 1, ref mii);
        }

        int PopulateMenu(uint hMenu, int id)
        {
            // Grab some info about the file
            bool done = ProcessBatchResults(); 

            if (done)
            {
                AddMenuItem(hMenu, "Reschedule", id, 0);
                AddMenuItem(hMenu, "Retry Now", ++id, 1);
                AddMenuItem(hMenu, "Cancel", ++id, 2);
            }
            else
            {
                // Uses 100-baed values to distinguish on the "done" status
                AddMenuItem(hMenu, "Commit", 100 + id, 0);
                AddMenuItem(hMenu, "Rollback", 100 + (++id), 1);
            }

            return id++;
        }

        bool ProcessBatchResults()
        {
            FileInfo fi = new FileInfo(m_fileName);
            return (fi.Length >0);
        }
```

## Sample Code:
```cs
void IContextMenu.GetCommandString(int idCmd, uint uFlags, int pwReserved, StringBuilder commandString, int cchMax)
        {
            switch(uFlags)
            {
            case (uint)GCS.VERB:
                commandString = new StringBuilder("...");
                break;
            case (uint)GCS.HELPTEXT:
                commandString = new StringBuilder("..."); 
                break;
            }
        }
```

## Sample Code:
```cs
void IContextMenu.InvokeCommand (IntPtr pici)
        {
            try
            {
                Type typINVOKECOMMANDINFO = Type.GetType("ShellExt.INVOKECOMMANDINFO");
                INVOKECOMMANDINFO ici = (INVOKECOMMANDINFO)Marshal.PtrToStructure(pici, typINVOKECOMMANDINFO);
                switch (ici.verb-1)
                {
                    case 0:
                        RescheduleJob();
                        break;
                    case 1:
                        RetryNowJob();
                        break;
                    case 2:
                        CancelJob();
                        break;
                    case 100:
                        CommitJob();
                        break;
                    case 101:
                        RollbackJob();
                        break;
                }
            }
            catch(Exception)
            {
            }
        }
        #endregion

        #region IShellExtInit
        int    IShellExtInit.Initialize (IntPtr pidlFolder, IntPtr lpdobj, uint hKeyProgID)
        {
            try
            {
                if (lpdobj != (IntPtr)0)
                {
                    // Get info about the directory
                    IDataObject dataObject = (IDataObject)Marshal.GetObjectForIUnknown(lpdobj);
                    FORMATETC fmt = new FORMATETC();
                    fmt.cfFormat = CLIPFORMAT.CF_HDROP;
                    fmt.ptd         = 0;
                    fmt.dwAspect = DVASPECT.DVASPECT_CONTENT;
                    fmt.lindex     = -1;
                    fmt.tymed     = TYMED.TYMED_HGLOBAL;
                    STGMEDIUM medium = new STGMEDIUM();
                    dataObject.GetData(ref fmt, ref medium);
                    m_hDrop = medium.hGlobal;
                }
            }
            catch(Exception)
            {
            }
            return 0;
        }

        #endregion

        #region Private Members
        private    void CancelJob()
        {
            MessageBox.Show("Gotta cancel the job", Path.GetFileName(m_fileName));
        }
        private    void RescheduleJob()
        {
            MessageBox.Show("Gotta reschedule the job", Path.GetFileName(m_fileName));
        }
        private    void RetryNowJob()
        {
            MessageBox.Show("Gotta retry the job NOW", Path.GetFileName(m_fileName));
        }
        private    void CommitJob()
        {
            MessageBox.Show("Gotta commit the job", Path.GetFileName(m_fileName));
        }
        private    void RollbackJob()
        {
            MessageBox.Show("Gotta rollback the job", Path.GetFileName(m_fileName));
        }
        #endregion

        #region Registration
        [System.Runtime.InteropServices.ComRegisterFunctionAttribute()]
        public static void RegisterServer(String str1)
        {
            try
            {
                // For Winnt set me as an approved shellex
                RegistryKey root;
                RegistryKey rk;
                root = Registry.LocalMachine;
                rk = root.OpenSubKey("Software\\Microsoft\\Windows\\CurrentVersion\\Shell Extensions\\Approved", true);
                rk.SetValue(guid.ToString(), "BatchResults shell extension");
                rk.Close();

                // Set "Folder\\shellex\\ContextMenuHandlers\\BatchResults" regkey to my guid
                root = Registry.ClassesRoot;
                rk = root.CreateSubKey("POPUPTEST\\shellex\\ContextMenuHandlers\\BatchResults");
                rk.SetValue("", guid.ToString());
                rk.Close();
            }
            catch(Exception e)
            {
                System.Console.WriteLine(e.ToString());
            }
        }

        [System.Runtime.InteropServices.ComUnregisterFunctionAttribute()]
        public static void UnregisterServer(String str1)
        {
            try
            {
                RegistryKey root;
                RegistryKey rk;

                // Remove ShellExtenstions registration
                root = Registry.LocalMachine;
                rk = root.OpenSubKey("Software\\Microsoft\\Windows\\CurrentVersion\\Shell Extensions\\Approved", true);
                rk.DeleteValue(guid);
                rk.Close();

                // Delete  regkey
                root = Registry.ClassesRoot;
                root.DeleteSubKey("POPUPTEST\\shellex\\ContextMenuHandlers\\BatchResults");
            }
            catch(Exception e)
            {
                System.Console.WriteLine(e.ToString());
            }
        }
        #endregion

    }
```

## Sample Code:
```cs
public class Helpers
    {
    public const uint WM_DRAWITEM = 0x002b;
    public const uint WM_MEASUREITEM = 0x002c;
```

## Sample Code:
```cs
[DllImport("shell32")]
    internal static extern uint DragQueryFile(uint hDrop, uint iFile, StringBuilder buffer, int cch);
```

## Sample Code:
```cs
[DllImport("user32")]
    internal static extern HMenu CreatePopupMenu();

    [DllImport("user32")]
    internal static extern bool InsertMenuItem(HMenu hmenu, uint uposition, uint uflags, ref MENUITEMINFO mii);

    [DllImport("user32")]
    internal static extern bool AppendMenu(HMenu hmenu, MFMENU uflags, IntPtr uIDNewItemOrSubmenu, string text);

    [DllImport("user32")]
    internal static extern bool InsertMenu(HMenu hmenu, int position, MFMENU uflags, IntPtr uIDNewItemOrSubmenu, string text);

    [DllImport("user32")]
    internal static extern int SetMenuItemBitmaps(HMenu hmenu, int nPosition, MFMENU uflags, IntPtr hBitmapUnchecked, IntPtr hBitmapChecked);
    }
```
