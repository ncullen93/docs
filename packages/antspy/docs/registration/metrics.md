Module ants.registration.metrics
================================

Functions
---------

    
`image_mutual_information(image1, image2)`
:   Compute mutual information between two ANTsImage types
    
    ANTsR function: `antsImageMutualInformation`
    
    Arguments
    ---------
    image1 : ANTsImage
        image 1
    
    image2 : ANTsImage
        image 2
    
    Returns
    -------
    scalar
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read( ants.get_ants_data('r16') ).clone('float')
    >>> mi = ants.image_read( ants.get_ants_data('r64') ).clone('float')
    >>> mival = ants.image_mutual_information(fi, mi) # -0.1796141