Module ants.registration.reflect_image
======================================

Functions
---------

    
`reflect_image(image, axis=None, tx=None, metric='mattes')`
:   Reflect an image along an axis
    
    ANTsR function: `reflectImage`
    
    Arguments
    ---------
    image : ANTsImage
        image to reflect
    
    axis : integer (optional)
        which dimension to reflect across, numbered from 0 to imageDimension-1
    
    tx : string (optional)
        transformation type to estimate after reflection
    
    metric : string  
        similarity metric for image registration. see antsRegistration.
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read( ants.get_ants_data('r16'), 'float' )
    >>> axis = 2
    >>> asym = ants.reflect_image(fi, axis, 'Affine')['warpedmovout']
    >>> asym = asym - fi