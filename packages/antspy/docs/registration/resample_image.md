Module ants.registration.resample_image
=======================================

Functions
---------

    
`resample_image(image, resample_params, use_voxels=False, interp_type=1)`
:   Resample image by spacing or number of voxels with
    various interpolators. Works with multi-channel images.
    
    ANTsR function: `resampleImage`
    
    Arguments
    ---------
    image : ANTsImage
        input image
    
    resample_params : tuple/list
        vector of size dimension with numeric values
    
    use_voxels : boolean
        True means interpret resample params as voxel counts
    
    interp_type : integer
        one of 0 (linear), 1 (nearest neighbor), 2 (gaussian), 3 (windowed sinc), 4 (bspline)
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read( ants.get_ants_data("r16"))
    >>> finn = ants.resample_image(fi,(50,60),True,0)
    >>> filin = ants.resample_image(fi,(1.5,1.5),False,1)

    
`resample_image_to_target(image, target, interp_type='linear', imagetype=0, verbose=False, **kwargs)`
:   Resample image by using another image as target reference.
    This function uses ants.apply_transform with an identity matrix
    to achieve proper resampling.
    
    ANTsR function: `resampleImageToTarget`
    
    Arguments
    ---------
    image : ANTsImage
        image to resample
    
    target : ANTsImage
        image of reference, the output will be in this space
    
    interp_type : string
        Choice of interpolator. Supports partial matching.
            linear
            nearestNeighbor
            multiLabel for label images but genericlabel is preferred
            gaussian
            bSpline
            cosineWindowedSinc
            welchWindowedSinc
            hammingWindowedSinc
            lanczosWindowedSinc
            genericLabel use this for label images
    
    imagetype : integer
        choose 0/1/2/3 mapping to scalar/vector/tensor/time-series
    
    verbose : boolean
        print command and run verbose application of transform.
    
    kwargs : keyword arguments
        additional arugment passed to antsApplyTransforms C code
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read(ants.get_ants_data('r16'))
    >>> fi2mm = ants.resample_image(fi, (2,2), use_voxels=0, interp_type='linear')
    >>> resampled = ants.resample_image_to_target(fi2mm, fi, verbose=True)