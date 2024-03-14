Module ants.core.ants_transform_io
==================================

Functions
---------

    
`create_ants_transform(transform_type='AffineTransform', precision='float', dimension=3, matrix=None, offset=None, center=None, translation=None, parameters=None, fixed_parameters=None, displacement_field=None, supported_types=False)`
:   Create and initialize an ANTsTransform
    
    ANTsR function: `createAntsrTransform`
    
    Arguments
    ---------
    transform_type : string
        type of transform(s)
    
    precision : string
        numerical precision
    
    dimension : integer
        spatial dimension of transform
    
    matrix : ndarray
        matrix for linear transforms
    
    offset : tuple/list
        offset for linear transforms
    
    center : tuple/list
        center for linear transforms
    
    translation : tuple/list
        translation for linear transforms
    
    parameters : ndarray/list
        array of parameters
    
    fixed_parameters : ndarray/list
        array of fixed parameters
    
    displacement_field : ANTsImage
        multichannel ANTsImage for non-linear transform
    
    supported_types : boolean
        flag that returns array of possible transforms types
    
    Returns
    -------
    ANTsTransform or list of ANTsTransform types
    
    Example
    -------
    >>> import ants
    >>> translation = (3,4,5)
    >>> tx = ants.create_ants_transform( type='Euler3DTransform', translation=translation )

    
`new_ants_transform(precision='float', dimension=3, transform_type='AffineTransform', parameters=None, fixed_parameters=None)`
:   Create a new ANTsTransform
    
    ANTsR function: None
    
    This is a simplified method for creating an ANTsTransform, mostly used internally.
    See create_ants_transform for more options.
    
    Example
    -------
    >>> import ants
    >>> tx = ants.new_ants_transform()

    
`read_transform(filename, precision='float')`
:   Read a transform from file
    
    ANTsR function: `readAntsrTransform`
    
    Arguments
    ---------
    filename : string
        filename of transform
    
    precision : string
        numerical precision of transform
    
    Returns
    -------
    ANTsTransform
    
    Example
    -------
    >>> import ants
    >>> tx = ants.new_ants_transform(dimension=2)
    >>> tx.set_parameters((0.9,0,0,1.1,10,11))
    >>> ants.write_transform(tx, '~/desktop/tx.mat')
    >>> tx2 = ants.read_transform('~/desktop/tx.mat')

    
`transform_from_displacement_field(field)`
:   Convert deformation field (multiChannel image) to ANTsTransform
    
    ANTsR function: `antsrTransformFromDisplacementField`
    
    Arguments
    ---------
    field : ANTsImage
        deformation field as multi-channel ANTsImage
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read(ants.get_ants_data('r16') )
    >>> mi = ants.image_read(ants.get_ants_data('r64') )
    >>> fi = ants.resample_image(fi,(60,60),1,0)
    >>> mi = ants.resample_image(mi,(60,60),1,0) # speed up
    >>> mytx = ants.registration(fixed=fi, moving=mi, type_of_transform = ('SyN') )
    >>> vec = ants.image_read( mytx['fwdtransforms'][0] )
    >>> atx = ants.transform_from_displacement_field( vec )

    
`transform_to_displacement_field(xfrm, ref)`
:   Convert displacement field ANTsTransform to displacement field
    
    ANTsR function: `antsrTransformToDisplacementField`
    
    Arguments
    ---------
    xfrm : displacement field ANTsTransform
        displacement field ANTsTransform
    
    ref : ANTs Image
    
    Returns
    -------
    ANTsVectorImage
    
    Example
    -------
    >>> import ants
    >>> fi = ants.image_read(ants.get_ants_data('r16') )
    >>> mi = ants.image_read(ants.get_ants_data('r64') )
    >>> fi = ants.resample_image(fi,(60,60),1,0)
    >>> mi = ants.resample_image(mi,(60,60),1,0) # speed up
    >>> mytx = ants.registration(fixed=fi, moving=mi, type_of_transform = ('SyN') )
    >>> vec = ants.image_read( mytx['fwdtransforms'][0] )
    >>> atx = ants.transform_from_displacement_field( vec )
    >>> field = ants.transform_to_displacement_field( atx, fi )

    
`write_transform(transform, filename)`
:   Write ANTsTransform to file
    
    ANTsR function: `writeAntsrTransform`
    
    Arguments
    ---------
    transform : ANTsTransform
        transform to save
    
    filename : string
        filename of transform (file extension is ".mat" for affine transforms)
    
    Returns
    -------
    N/A
    
    Example
    -------
    >>> import ants
    >>> tx = ants.new_ants_transform(dimension=2)
    >>> tx.set_parameters((0.9,0,0,1.1,10,11))
    >>> ants.write_transform(tx, '~/desktop/tx.mat')
    >>> tx2 = ants.read_transform('~/desktop/tx.mat')