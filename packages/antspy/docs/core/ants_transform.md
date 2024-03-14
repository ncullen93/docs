Module ants.core.ants_transform
===============================

Functions
---------

    
`apply_ants_transform(transform, data, data_type='point', reference=None, **kwargs)`
:   Apply ANTsTransform to data
    
    ANTsR function: `applyAntsrTransform`
    
    Arguments
    ---------
    transform : ANTsTransform
        transform to apply to image
    
    data : ndarray/list/tuple
        data to which transform will be applied
    
    data_type : string
        type of data
        Options :
            'point'
            'vector'
            'image'
    
    reference : ANTsImage
        target space for transforming image
    
    kwargs : kwargs
        additional options passed to `apply_ants_transform_to_image`
    
    Returns
    -------
    ANTsImage if data_type == 'point'
    OR
    tuple if data_type == 'point' or data_type == 'vector'

    
`apply_ants_transform_to_image(transform, image, reference, interpolation='linear')`
:   Apply transform to an image
    
    ANTsR function: `applyAntsrTransformToImage`
    
    Arguments
    ---------
    image : ANTsImage
        image to which the transform will be applied
    
    reference : ANTsImage
        reference image
    
    interpolation : string
        type of interpolation to use. Options are:
        linear
        nearestneighbor
        multilabel
        gaussian
        bspline
        cosinewindowedsinc
        welchwindowedsinc
        hammingwindoweddinc
        lanczoswindowedsinc
        genericlabel
    
    Returns
    -------
    list : transformed vector
    
    Example
    -------
    >>> import ants
    >>> img = ants.image_read(ants.get_ants_data("r16")).clone('float')
    >>> tx = ants.new_ants_transform(dimension=2)
    >>> tx.set_parameters((0.9,0,0,1.1,10,11))
    >>> img2 = tx.apply_to_image(img, img)

    
`apply_ants_transform_to_point(transform, point)`
:   Apply transform to a point
    
    ANTsR function: `applyAntsrTransformToPoint`
    
    Arguments
    ---------
    point : list/tuple
        point to which the transform will be applied
    
    Returns
    -------
    tuple : transformed point
    
    Example
    -------
    >>> import ants
    >>> tx = ants.new_ants_transform()
    >>> params = tx.parameters
    >>> tx.set_parameters(params*2)
    >>> pt2 = tx.apply_to_point((1,2,3)) # should be (2,4,6)

    
`apply_ants_transform_to_vector(transform, vector)`
:   Apply transform to a vector
    
    ANTsR function: `applyAntsrTransformToVector`
    
    Arguments
    ---------
    vector : list/tuple
        vector to which the transform will be applied
    
    Returns
    -------
    tuple : transformed vector

    
`compose_ants_transforms(transform_list)`
:   Compose multiple ANTsTransform's together
    
    ANTsR function: `composeAntsrTransforms`
    
    Arguments
    ---------
    transform_list : list/tuple of ANTsTransform object
        list of transforms to compose together
    
    Returns
    -------
    ANTsTransform
        one transform that contains all given transforms
    
    Example
    -------
    >>> import ants
    >>> img = ants.image_read(ants.get_ants_data("r16")).clone('float')
    >>> tx = ants.new_ants_transform(dimension=2)
    >>> tx.set_parameters((0.9,0,0,1.1,10,11))
    >>> inv_tx = tx.invert()
    >>> single_tx = ants.compose_ants_transforms([tx, inv_tx])
    >>> img_orig = single_tx.apply_to_image(img, img)
    >>> rRotGenerator = ants.contrib.RandomRotate2D( ( 0, 40 ), reference=img )
    >>> rShearGenerator=ants.contrib.RandomShear2D( (0,50), reference=img )
    >>> tx1 = rRotGenerator.transform()
    >>> tx2 = rShearGenerator.transform()
    >>> rSrR = ants.compose_ants_transforms([tx1, tx2])
    >>> rSrR.apply_to_image( img )

    
`get_ants_transform_fixed_parameters(transform)`
:   Get fixed parameters of an ANTsTransform
    
    ANTsR function: `getAntsrTransformFixedParameters`

    
`get_ants_transform_parameters(transform)`
:   Get parameters of an ANTsTransform
    
    ANTsR function: `getAntsrTransformParameters`

    
`invert_ants_transform(transform)`
:   Invert ANTsTransform
    
    ANTsR function: `invertAntsrTransform`
    
    Example
    -------
    >>> import ants
    >>> img = ants.image_read(ants.get_ants_data("r16")).clone('float')
    >>> tx = ants.new_ants_transform(dimension=2)
    >>> tx.set_parameters((0.9,0,0,1.1,10,11))
    >>> img_transformed = tx.apply_to_image(img, img)
    >>> inv_tx = tx.invert()
    >>> img_orig = inv_tx.apply_to_image(img_transformed, img_transformed)

    
`set_ants_transform_fixed_parameters(transform, parameters)`
:   Set fixed parameters of an ANTsTransform
    
    ANTsR function: `setAntsrTransformFixedParameters`

    
`set_ants_transform_parameters(transform, parameters)`
:   Set parameters of an ANTsTransform
    
    ANTsR function: `setAntsrTransformParameters`

    
`transform_index_to_physical_point(image, index)`
:   Get spatial point from index of an image.
    
    ANTsR function: `antsTransformIndexToPhysicalPoint`
    
    Arguments
    ---------
    img : ANTsImage
        image to get values from
    
    index : list or tuple or numpy.ndarray
        location in image
    
    Returns
    -------
    tuple
    
    Example
    -------
    >>> import ants
    >>> import numpy as np
    >>> img = ants.make_image((10,10),np.random.randn(100))
    >>> pt = ants.transform_index_to_physical_point(img, (2,2))

    
`transform_physical_point_to_index(image, point)`
:   Get index from spatial point of an image.
    
    ANTsR function: `antsTransformPhysicalPointToIndex`
    
    Arguments
    ---------
    image : ANTsImage
        image to get values from
    
    point : list or tuple or numpy.ndarray
        point in image
    
    Returns
    -------
    tuple
    
    Example
    -------
    >>> import ants
    >>> import numpy as np
    >>> img = ants.make_image((10,10),np.random.randn(100))
    >>> idx = ants.transform_physical_point_to_index(img, (2,2))
    >>> img.set_spacing((2,2))
    >>> idx2 = ants.transform_physical_point_to_index(img, (4,4))

Classes
-------

`ANTsTransform(precision='float', dimension=3, transform_type='AffineTransform', pointer=None)`
:   NOTE: This class should never be initialized directly by the user.
    
    Initialize an ANTsTransform object.
    
    Arguments
    ---------
    pixeltype : string
    
    dimension : integer
    
    transform_type : stirng
    
    pointer : py::capsule (optional)

    ### Instance variables

    `fixed_parameters`
    :   Get parameters of transform

    `parameters`
    :   Get parameters of transform

    ### Methods

    `apply(self, data, data_type='point', reference=None, **kwargs)`
    :   Apply transform to data

    `apply_to_image(self, image, reference=None, interpolation='linear')`
    :   Apply transform to an image
        
        Arguments
        ---------
        image : ANTsImage
            image to which the transform will be applied
        
        reference : ANTsImage
            target space for transforming image
        
        interpolation : string
            type of interpolation to use. Options are:
                linear
                nearestneighbor
                multilabel
                gaussian
                bspline
                cosinewindowedsinc
                welchwindowedsinc
                hammingwindoweddinc
                lanczoswindowedsinc
                genericlabel
        
        Returns
        -------
        list : transformed vector

    `apply_to_point(self, point)`
    :   Apply transform to a point
        
        Arguments
        ---------
        point : list/tuple
            point to which the transform will be applied
        
        Returns
        -------
        list : transformed point
        
        Example
        -------
        >>> import ants
        >>> tx = ants.new_ants_transform()
        >>> params = tx.parameters
        >>> tx.set_parameters(params*2)
        >>> pt2 = tx.apply_to_point((1,2,3)) # should be (2,4,6)

    `apply_to_vector(self, vector)`
    :   Apply transform to a vector
        
        Arguments
        ---------
        vector : list/tuple
            vector to which the transform will be applied
        
        Returns
        -------
        list : transformed vector

    `invert(self)`
    :   Invert the transform

    `set_fixed_parameters(self, parameters)`
    :   Set parameters of transform

    `set_parameters(self, parameters)`
    :   Set parameters of transform