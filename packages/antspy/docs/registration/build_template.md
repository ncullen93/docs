Module ants.registration.build_template
=======================================

Functions
---------

    
`build_template(initial_template=None, image_list=None, iterations=3, gradient_step=0.2, blending_weight=0.75, weights=None, useNoRigid=True, **kwargs)`
:   Estimate an optimal template from an input image_list
    
    ANTsR function: N/A
    
    Arguments
    ---------
    initial_template : ANTsImage
        initialization for the template building
    
    image_list : ANTsImages
        images from which to estimate template
    
    iterations : integer
        number of template building iterations
    
    gradient_step : scalar
        for shape update gradient
    
    blending_weight : scalar
        weight for image blending
    
    weights : vector
        weight for each input image
    
    useNoRigid : boolean
        equivalent of -y in the script. Template update
        step will not use the rigid component if this is True.
    kwargs : keyword args
        extra arguments passed to ants registration
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> image = ants.image_read( ants.get_ants_data('r16') )
    >>> image2 = ants.image_read( ants.get_ants_data('r27') )
    >>> image3 = ants.image_read( ants.get_ants_data('r85') )
    >>> timage = ants.build_template( image_list = ( image, image2, image3 ) ).resample_image( (45,45))
    >>> timagew = ants.build_template( image_list = ( image, image2, image3 ), weights = (5,1,1) )