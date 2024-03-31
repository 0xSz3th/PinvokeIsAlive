
## C# Definition:
```cs
/// <summary>
    /// The IObjectWithSite Interface provides simple objects with a lightweight siting mechanism. 
    /// </summary>
    /// <remarks>
    /// Often, an object needs to communicate directly with a container site that is managing the 
    /// object itself. Outside of IOleObject::SetClientSite, there is no generic means through 
    /// which an object becomes aware of its site. IObjectWithSite provides a siting mechanism. 
    /// This interface should only be used when IOleObject is not already in use. Through 
    /// <see cref="IObjectWithSite"/>, a container can pass the IUnknown pointer of its site to the 
    /// object through <see cref="SetSite"/>. Callers can also retrieve the latest site passed 
    /// to <see cref="SetSite"/> through <see cref="GetSite"/>. 
    /// </remarks>
    [ComImport, Guid("FC4801A3-2BA9-11CF-A229-00AA003D7352"), InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IObjectWithSite
    {
    /// <summary>
    /// Provides the site's <see cref="IUnknown"/> pointer to the object.
    /// </summary>
    /// <param name="pUnkSite">The site managing this object. If NULL, the object should call 
    /// <see cref="IUnknown.Release">IUnknown.Release</see>to release the existing site.</param>
    /// <remarks>
    /// The object should hold onto the <see cref="IUnknown"/> pointer, calling <c>AddRef</c> in doing so. 
    /// If the object already has a site, it should first call <c>AddRef</c> to secure the 
    /// new site, call <c>Release</c> on the existing site, and then save <paramref name="pUnkSite"/>.
    /// <para>
    /// E_NOTIMPL is disallowed—without implementation of <see cref="SetSite"/>, the 
    /// <see cref="IObjectWithSite"/> interface is unnecessary.
    /// </para>
    /// </remarks>
    void SetSite([In, MarshalAs(UnmanagedType.IUnknown)] object pUnkSite);

    /// <summary>
    /// Retrieves the last site set with <see cref="SetSite"/>. If there's no known site, 
    /// the object returns a failure code.
    /// </summary>
    /// <param name="riid">The IID of the interface pointer that should be returned.</param>
    /// <returns>The object of the site last seen in <see cref="SetSite"/>.</returns>
    /// <remarks>
    /// The specific interface returned depends in the <paramref name="riid"/> argument—in essence, 
    /// the two arguments act identically to those in <c>QueryInterface</c>. If the appropriate 
    /// interface pointer is available, the object must call <c>AddRef</c> on that pointer before 
    /// returning successfully. If no site is available, or the requested interface is not supported, 
    /// the object sets this argument to NULL and returns a failure code.
    /// </remarks>
    [return: MarshalAs(UnmanagedType.IUnknown)]
    object GetSite([In] ref Guid riid);
    }
```

## VB Definition:
```cs
<ComImport(), SuppressUnmanagedCodeSecurity(), Guid("FC4801A3-2BA9-11CF-A229-00AA003D7352"), InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
Interface IObjectWithSite
    Sub SetSite(<MarshalAs(UnmanagedType.IUnknown)> ByVal pUnkSite As Object)
    Sub GetSite(ByRef riid As Guid, <MarshalAs(UnmanagedType.Interface)> ByRef ppvSite As Object)
End Interface
```
