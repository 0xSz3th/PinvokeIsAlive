
## C# Definition:
```cs
public struct WLAN_PROFILE_INFO_LIST
     {
        public uint dwNumberOfItems;
        public uint dwIndex;
        public WLAN_PROFILE_INFO[] ProfileInfo;

        public WLAN_PROFILE_INFO_LIST(IntPtr ppProfileList)
          {
            dwNumberOfItems = (uint)Marshal.ReadInt32(ppProfileList);
            dwIndex = (uint)Marshal.ReadInt32(ppProfileList, 4);
            ProfileInfo = new WLAN_PROFILE_INFO[dwNumberOfItems];
            IntPtr ppProfileListTemp = new IntPtr(ppProfileList.ToInt64() + 8);

            for (int i = 0; i < dwNumberOfItems; i++)
            {
                    ppProfileList = new IntPtr(ppProfileListTemp.ToInt64() + i * Marshal.SizeOf(typeof(WLAN_PROFILE_INFO)));
                    ProfileInfo[i] = (WLAN_PROFILE_INFO)Marshal.PtrToStructure(ppProfileList, typeof(WLAN_PROFILE_INFO));
            }
           }
     }
```

## VB Definition:
```cs
Structure WLAN_PROFILE_INFO_LIST 
   Public TODO
End Structure
```
