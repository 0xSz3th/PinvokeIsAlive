
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern bool TrackMouseEvent(ref TRACKMOUSEEVENT lpEventTrack);
```

## Sample Code:
```cs
// C#    
    // Sets the hover time to 3sec and resets MouseEnter so the cursor does not have to
    // leave the control to hover again 

        [DllImport("user32.dll")]
        static extern int TrackMouseEvent(ref TRACKMOUSEEVENT lpEventTrack);
        [StructLayout(LayoutKind.Sequential)]
        public struct TRACKMOUSEEVENT 
        {
            public Int32 cbSize;    // using Int32 instead of UInt32 is safe here, and this avoids casting the result  of Marshal.SizeOf()
            [MarshalAs(UnmanagedType.U4)]
            public TMEFlags dwFlags;
            public IntPtr hWnd;
            public UInt32 dwHoverTime;

            public TRACKMOUSEEVENT(Int32 dwFlags, IntPtr hWnd, UInt32 dwHoverTime)
            {
                this.cbSize = Marshal.SizeOf(typeof(TRACKMOUSEEVENT));
                this.dwFlags = dwFlags;
                this.hWnd = hWnd;
                this.dwHoverTime = dwHoverTime;
            }
        }        

        protected override void OnMouseHover(EventArgs e)
        {            
            OnMouseEnter(e);
            base.OnMouseHover(e);
        }

        TRACKMOUSEEVENT tme; // Define it on the outside so you dont recreate it each time the mouse enters
        protected override void OnMouseEnter(EventArgs e)
        {            
            base.OnMouseEnter(e);
            tme = new TRACKMOUSEEVENT();            
            tme.hWnd = this.Handle;            
            tme.cbSize = Marshal.SizeOf(typeof(TRACKMOUSEEVENT)); // make sure it gets correct size in different platforms
            tme.dwFlags = TMEFlags.TME_HOVER;
            tme.dwHoverTime = 1000 * 3;
            TrackMouseEvent(ref tme);            
        }

        /// <summary>
        /// The services requested. This member can be a combination of the following values. 
        /// </summary>
        /// <seealso cref="http://msdn.microsoft.com/en-us/library/ms645604%28v=vs.85%29.aspx"/>
        [Flags]
        public enum TMEFlags : uint
        {
            /// <summary>
            /// The caller wants to cancel a prior tracking request. The caller should also specify the type of tracking that it wants to cancel. For example, to cancel hover tracking, the caller must pass the TME_CANCEL and TME_HOVER flags.
            /// </summary>
            TME_CANCEL = 0x80000000,
            /// <summary>
            /// The caller wants hover notification. Notification is delivered as a WM_MOUSEHOVER message.
            /// If the caller requests hover tracking while hover tracking is already active, the hover timer will be reset.
            /// This flag is ignored if the mouse pointer is not over the specified window or area.
            /// </summary>
            TME_HOVER = 0x00000001,
            /// <summary>
            /// The caller wants leave notification. Notification is delivered as a WM_MOUSELEAVE message. If the mouse is not over the specified window or area, a leave notification is generated immediately and no further tracking is performed.
            /// </summary>
            TME_LEAVE = 0x00000002,
            /// <summary>
            /// The caller wants hover and leave notification for the nonclient areas. Notification is delivered as WM_NCMOUSEHOVER and WM_NCMOUSELEAVE messages.
            /// </summary>
            TME_NONCLIENT = 0x00000010,
            /// <summary>
            /// The function fills in the structure instead of treating it as a tracking request. The structure is filled such that had that structure been passed to TrackMouseEvent, it would generate the current tracking. The only anomaly is that the hover time-out returned is always the actual time-out and not HOVER_DEFAULT, if HOVER_DEFAULT was specified during the original TrackMouseEvent request. 
            /// </summary>
            TME_QUERY = 0x40000000,
        }
```
