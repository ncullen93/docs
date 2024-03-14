Module ants.core.ants_image_io
==============================
Image IO

Functions
---------

    
`_from_numpy(data, origin=None, spacing=None, direction=None, has_components=False, is_rgb=False)`
:   Internal function for creating an ANTsImage

    
`dicom_read(directory, pixeltype='float')`
:   Read a set of dicom files in a directory into a single ANTsImage.
    The origin of the resulting 3D image will be the origin of the
    first dicom image read.
    
    Arguments
    ---------
    directory : string
        folder in which all the dicom images exist
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> img = ants.dicom_read('~/desktop/dicom-subject/')

    
`from_numpy(data, origin=None, spacing=None, direction=None, has_components=False, is_rgb=False)`
:   Create an ANTsImage object from a numpy array
    
    ANTsR function: `as.antsImage`
    
    Arguments
    ---------
    data : ndarray
        image data array
    
    origin : tuple/list
        image origin
    
    spacing : tuple/list
        image spacing
    
    direction : list/ndarray
        image direction
    
    has_components : boolean
        whether the image has components
    
    Returns
    -------
    ANTsImage
        image with given data and any given information

    
`image_clone(image, pixeltype=None)`
:   Clone an ANTsImage
    
    ANTsR function: `antsImageClone`
    
    Arguments
    ---------
    image : ANTsImage
        image to clone
    
    dtype : string (optional)
        new datatype for image
    
    Returns
    -------
    ANTsImage

    
`image_header_info(filename)`
:   Read file info from image header
    
    ANTsR function: `antsImageHeaderInfo`
    
    Arguments
    ---------
    filename : string
        name of image file from which info will be read
    
    Returns
    -------
    dict

    
`image_list_to_matrix(image_list, mask=None, sigma=None, epsilon=0.5)`
:   Read images into rows of a matrix, given a mask - much faster for
    large datasets as it is based on C++ implementations.
    
    ANTsR function: `imagesToMatrix`
    
    Arguments
    ---------
    image_list : list of ANTsImage types
        images to convert to ndarray
    
    mask : ANTsImage (optional)
        image containing binary mask. voxels in the mask are placed in the matrix
    
    sigma : scaler (optional)
        smoothing factor
    
    epsilon : scalar
        threshold for mask
    
    Returns
    -------
    ndarray
        array with a row for each image
        shape = (N_IMAGES, N_VOXELS)
    
    Example
    -------
    >>> import ants
    >>> img = ants.image_read(ants.get_ants_data('r16'))
    >>> img2 = ants.image_read(ants.get_ants_data('r16'))
    >>> img3 = ants.image_read(ants.get_ants_data('r16'))
    >>> mat = ants.image_list_to_matrix([img,img2,img3])

    
`image_read(filename, dimension=None, pixeltype='float', reorient=False)`
:   Read an ANTsImage from file
    
    ANTsR function: `antsImageRead`
    
    Arguments
    ---------
    filename : string
        Name of the file to read the image from.
    
    dimension : int
        Number of dimensions of the image read. This need not be the same as
        the dimensions of the image in the file. Allowed values: 2, 3, 4.
        If not provided, the dimension is obtained from the image file
    
    pixeltype : string
        C++ datatype to be used to represent the pixels read. This datatype
        need not be the same as the datatype used in the file.
        Options: unsigned char, unsigned int, float, double
    
    reorient : boolean | string
        if True, the image will be reoriented to RPI if it is 3D
        if False, nothing will happen
        if string, this should be the 3-letter orientation to which the
            input image will reoriented if 3D.
        if the image is 2D, this argument is ignored
    
    Returns
    -------
    ANTsImage

    
`image_write(image, filename, ri=False)`
:   Write an ANTsImage to file
    
    ANTsR function: `antsImageWrite`
    
    Arguments
    ---------
    image : ANTsImage
        image to save to file
    
    filename : string
        name of file to which image will be saved
    
    ri : boolean
        if True, return image. This allows for using this function in a pipeline:
            >>> img2 = img.smooth_image(2.).image_write(file1, ri=True).threshold_image(0,20).image_write(file2, ri=True)
        if False, do not return image

    
`images_from_matrix(data_matrix, mask)`
:   Unmasks rows of a matrix and writes as images
    
    ANTsR function: `matrixToImages`
    
    Arguments
    ---------
    data_matrix : numpy.ndarray
        each row corresponds to an image
        array should have number of columns equal to non-zero voxels in the mask
    
    mask : ANTsImage
        image containing a binary mask. Rows of the matrix are
        unmasked and written as images. The mask defines the output image space
    
    Returns
    -------
    list of ANTsImage types
    
    Example
    -------
    >>> import ants
    >>> img = ants.image_read(ants.get_ants_data('r16'))
    >>> msk = ants.get_mask( img )
    >>> img2 = ants.image_read(ants.get_ants_data('r16'))
    >>> img3 = ants.image_read(ants.get_ants_data('r16'))
    >>> mat = ants.image_list_to_matrix([img,img2,img3], msk )
    >>> ilist = ants.matrix_to_images( mat, msk )

    
`images_to_matrix(image_list, mask=None, sigma=None, epsilon=0.5)`
:   Read images into rows of a matrix, given a mask - much faster for
    large datasets as it is based on C++ implementations.
    
    ANTsR function: `imagesToMatrix`
    
    Arguments
    ---------
    image_list : list of ANTsImage types
        images to convert to ndarray
    
    mask : ANTsImage (optional)
        image containing binary mask. voxels in the mask are placed in the matrix
    
    sigma : scaler (optional)
        smoothing factor
    
    epsilon : scalar
        threshold for mask
    
    Returns
    -------
    ndarray
        array with a row for each image
        shape = (N_IMAGES, N_VOXELS)
    
    Example
    -------
    >>> import ants
    >>> img = ants.image_read(ants.get_ants_data('r16'))
    >>> img2 = ants.image_read(ants.get_ants_data('r16'))
    >>> img3 = ants.image_read(ants.get_ants_data('r16'))
    >>> mat = ants.image_list_to_matrix([img,img2,img3])

    
`make_image(imagesize, voxval=0, spacing=None, origin=None, direction=None, has_components=False, pixeltype='float')`
:   Make an image with given size and voxel value or given a mask and vector
    
    ANTsR function: `makeImage`
    
    Arguments
    ---------
    shape : tuple/ANTsImage
        input image size or mask
    
    voxval : scalar
        input image value or vector, size of mask
    
    spacing : tuple/list
        image spatial resolution
    
    origin  : tuple/list
        image spatial origin
    
    direction : list/ndarray
        direction matrix to convert from index to physical space
    
    components : boolean
        whether there are components per pixel or not
    
    pixeltype : float
        data type of image values
    
    Returns
    -------
    ANTsImage

    
`matrix_from_images(image_list, mask=None, sigma=None, epsilon=0.5)`
:   Read images into rows of a matrix, given a mask - much faster for
    large datasets as it is based on C++ implementations.
    
    ANTsR function: `imagesToMatrix`
    
    Arguments
    ---------
    image_list : list of ANTsImage types
        images to convert to ndarray
    
    mask : ANTsImage (optional)
        image containing binary mask. voxels in the mask are placed in the matrix
    
    sigma : scaler (optional)
        smoothing factor
    
    epsilon : scalar
        threshold for mask
    
    Returns
    -------
    ndarray
        array with a row for each image
        shape = (N_IMAGES, N_VOXELS)
    
    Example
    -------
    >>> import ants
    >>> img = ants.image_read(ants.get_ants_data('r16'))
    >>> img2 = ants.image_read(ants.get_ants_data('r16'))
    >>> img3 = ants.image_read(ants.get_ants_data('r16'))
    >>> mat = ants.image_list_to_matrix([img,img2,img3])

    
`matrix_to_images(data_matrix, mask)`
:   Unmasks rows of a matrix and writes as images
    
    ANTsR function: `matrixToImages`
    
    Arguments
    ---------
    data_matrix : numpy.ndarray
        each row corresponds to an image
        array should have number of columns equal to non-zero voxels in the mask
    
    mask : ANTsImage
        image containing a binary mask. Rows of the matrix are
        unmasked and written as images. The mask defines the output image space
    
    Returns
    -------
    list of ANTsImage types
    
    Example
    -------
    >>> import ants
    >>> img = ants.image_read(ants.get_ants_data('r16'))
    >>> msk = ants.get_mask( img )
    >>> img2 = ants.image_read(ants.get_ants_data('r16'))
    >>> img3 = ants.image_read(ants.get_ants_data('r16'))
    >>> mat = ants.image_list_to_matrix([img,img2,img3], msk )
    >>> ilist = ants.matrix_to_images( mat, msk )

    
`matrix_to_timeseries(image, matrix, mask=None)`
:   converts a matrix to a ND image.
    
    ANTsR function: `matrix2timeseries`
    
    Arguments
    ---------
    
    image: reference ND image
    
    matrix: matrix to convert to image
    
    mask: mask image defining voxels of interest
    
    
    Returns
    -------
    ANTsImage
    
    Example
    -------
    >>> import ants
    >>> img = ants.make_image( (10,10,10,5 ) )
    >>> mask = ants.ndimage_to_list( img )[0] * 0
    >>> mask[ 4:8, 4:8, 4:8 ] = 1
    >>> mat = ants.timeseries_to_matrix( img, mask = mask )
    >>> img2 = ants.matrix_to_timeseries( img,  mat, mask)

    
`timeseries_to_matrix(image, mask=None)`
:   Convert a timeseries image into a matrix.
    
    ANTsR function: `timeseries2matrix`
    
    Arguments
    ---------
    image : image whose slices we convert to a matrix. E.g. a 3D image of size
           x by y by z will convert to a z by x*y sized matrix
    
    mask : ANTsImage (optional)
        image containing binary mask. voxels in the mask are placed in the matrix
    
    Returns
    -------
    ndarray
        array with a row for each image
        shape = (N_IMAGES, N_VOXELS)
    
    Example
    -------
    >>> import ants
    >>> img = ants.make_image( (10,10,10,5 ) )
    >>> mat = ants.timeseries_to_matrix( img )