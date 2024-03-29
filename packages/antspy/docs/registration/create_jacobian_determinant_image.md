Module ants.registration.create_jacobian_determinant_image
==========================================================

Functions
---------

    
`create_jacobian_determinant_image(domain_image, tx, do_log=False, geom=False)`
:   Compute the jacobian determinant from a transformation file
    
    ANTsR function: `createJacobianDeterminantImage`
    
    Arguments
    ---------
    domain_image : ANTsImage
        image that defines transformation domain
    
    tx : string
        deformation transformation file name
    
    do_log : boolean
        return the log jacobian
    
    geom : bolean
        use the geometric jacobian calculation (boolean)
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read( ants.get_ants_data('r16'))
    >>> mi = ants.image_read( ants.get_ants_data('r64'))
    >>> fi = ants.resample_image(fi,(128,128),1,0)
    >>> mi = ants.resample_image(mi,(128,128),1,0)
    >>> mytx = ants.registration(fixed=fi , moving=mi, type_of_transform = ('SyN') )
    >>> jac = ants.create_jacobian_determinant_image(fi,mytx['fwdtransforms'][0],1)

    
`deformation_gradient(warp_image, to_rotation=False, py_based=False)`
:   Compute the deformation gradient from an image containing a warp (deformation)
    
    ANTsR function: `NA`
    
    Arguments
    ---------
    warp_image : ANTsImage (or filename if not py_based)
        image that defines the deformation field (vector pixels)
    
    to_rotation : boolean maps deformation gradient to a rotation matrix
    
    py_based: boolean uses pure python implementation (maybe slow)
    
    Returns
    -------
    ANTsImage with dimension*dimension components indexed in order U_xyz, V_xyz, W_xyz 
        where U is the x-component of deformation and xyz are spatial.
    
    Note
    -------
    the to_rotation option is still experimental. use with caution.
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read( ants.get_ants_data('r16'))
    >>> mi = ants.image_read( ants.get_ants_data('r64'))
    >>> fi = ants.resample_image(fi,(128,128),1,0)
    >>> mi = ants.resample_image(mi,(128,128),1,0)
    >>> mytx = ants.registration(fixed=fi , moving=mi, type_of_transform = ('SyN') )
    >>> dg = ants.deformation_gradient( ants.image_read( mytx['fwdtransforms'][0] ) )