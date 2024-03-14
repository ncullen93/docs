Module ants.registration.fsl2antstransform
==========================================

Functions
---------

    
`fsl2antstransform(matrix, reference, moving)`
:   Convert an FSL linear transform to an antsrTransform
    
    ANTsR function: `fsl2antsrtransform`
    
    Arguments
    ---------
    matrix : ndarray/list
        4x4 matrix of transform parameters
    
    reference : ANTsImage
        target image
    
    moving : ANTsImage
        moving image
    
    Returns
    -------
    ANTsTransform
    
    Examples
    --------
    >>> import ants
    >>> import numpy as np
    >>> fslmat = np.zeros((4,4))
    >>> np.fill_diagonal(fslmat, 1)
    >>> img = ants.image_read(ants.get_ants_data('ch2'))
    >>> tx = ants.fsl2antstransform(fslmat, img, img)