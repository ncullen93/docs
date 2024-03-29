Module ants.registration.make_points_image
==========================================

Functions
---------

    
`make_points_image(pts, mask, radius=5)`
:   Create label image from physical space points
    
    Creates spherical points in the coordinate space of the target image based
    on the n-dimensional matrix of points that the user supplies. The image
    defines the dimensionality of the data so if the input image is 3D then
    the input points should be 2D or 3D.
    
    ANTsR function: `makePointsImage`
    
    Arguments
    ---------
    pts : numpy.ndarray
        input powers points
    
    mask : ANTsImage
        mask defining target space
    
    radius : integer
        radius for the points
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> import pandas as pd
    >>> mni = ants.image_read(ants.get_data('mni')).get_mask()
    >>> powers_pts = pd.read_csv(ants.get_data('powers_mni_itk'))
    >>> powers_labels = ants.make_points_image(powers_pts.iloc[:,:3].values, mni, radius=3)