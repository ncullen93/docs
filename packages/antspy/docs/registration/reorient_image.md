Module ants.registration.reorient_image
=======================================

Functions
---------

    
`get_center_of_mass(image)`
:   Compute an image center of mass in physical space which is defined
    as the mean of the intensity weighted voxel coordinate system.
    
    ANTsR function: `getCenterOfMass`
    
    Arguments
    ---------
    image : ANTsImage
        image from which center of mass will be computed
    
    Returns
    -------
    scalar
    
    Example
    -------
    >>> fi = ants.image_read( ants.get_ants_data("r16"))
    >>> com1 = ants.get_center_of_mass( fi )
    >>> fi = ants.image_read( ants.get_ants_data("r64"))
    >>> com2 = ants.get_center_of_mass( fi )

    
`get_orientation(image)`
:   

    
`get_possible_orientations()`
:   

    
`reorient_image2(image, orientation='RAS')`
:   Reorient an image.
    Example
    -------
    >>> import ants
    >>> mni = ants.image_read(ants.get_data('mni'))
    >>> mni2 = mni.reorient_image2()