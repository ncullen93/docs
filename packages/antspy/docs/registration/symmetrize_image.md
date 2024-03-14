Module ants.registration.symmetrize_image
=========================================

Functions
---------

    
`symmetrize_image(image)`
:   Use registration and reflection to make an image symmetric
    
    ANTsR function: N/A
    
    Arguments
    ---------
    image : ANTsImage
        image to make symmetric
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> image = ants.image_read( ants.get_ants_data('r16') , 'float')
    >>> simage = ants.symimage(image)