Module ants.core.ants_image
===========================

Functions
---------

    
`allclose(image1, image2)`
:   Check if two images have the same array values

    
`copy_image_info(reference, target)`
:   Copy origin, direction, and spacing from one antsImage to another
    
    ANTsR function: `antsCopyImageInfo`
    
    Arguments
    ---------
    reference : ANTsImage
        Image to get values from.
    target  : ANTsImAGE
        Image to copy values to
    
    Returns
    -------
    ANTsImage
        Target image with reference header information

    
`get_direction(image)`
:   Get direction of ANTsImage
    
    ANTsR function: `antsGetDirection`

    
`get_origin(image)`
:   Get origin of ANTsImage
    
    ANTsR function: `antsGetOrigin`

    
`get_spacing(image)`
:   Get spacing of ANTsImage
    
    ANTsR function: `antsGetSpacing`

    
`image_physical_space_consistency(image1, image2, tolerance=0.01, datatype=False)`
:   Check if two or more ANTsImage objects occupy the same physical space
    
    ANTsR function: `antsImagePhysicalSpaceConsistency`
    
    Arguments
    ---------
    *images : ANTsImages
        images to compare
    
    tolerance : float
        tolerance when checking origin and spacing
    
    data_type : boolean
        If true, also check that the image data types are the same
    
    Returns
    -------
    boolean
        true if images share same physical space, false otherwise

    
`image_type_cast(image_list, pixeltype=None)`
:   Cast a list of images to the highest pixeltype present in the list
    or all to a specified type
    
    ANTsR function: `antsImageTypeCast`
    
    Arguments
    ---------
    image_list : list/tuple
        images to cast
    
    pixeltype : string (optional)
        pixeltype to cast to. If None, images will be cast to the highest
        precision pixeltype found in image_list
    
    Returns
    -------
    list of ANTsImages
        given images casted to new type

    
`set_direction(image, direction)`
:   Set direction of ANTsImage
    
    ANTsR function: `antsSetDirection`

    
`set_origin(image, origin)`
:   Set origin of ANTsImage
    
    ANTsR function: `antsSetOrigin`

    
`set_spacing(image, spacing)`
:   Set spacing of ANTsImage
    
    ANTsR function: `antsSetSpacing`

Classes
-------

`ANTsImage(pixeltype='float', dimension=3, components=1, pointer=None, is_rgb=False, label_image=None)`
:   Initialize an ANTsImage
    
    Arguments
    ---------
    pixeltype : string
        ITK pixeltype of image
    
    dimension : integer
        number of image dimension. Does NOT include components dimension
    
    components : integer
        number of pixel components in the image
    
    pointer : py::capsule (optional)
        pybind11 capsule holding the pointer to the underlying ITK image object
    
    label_image : LabelImage
        a discrete label image for mapping locations to atlas regions

    ### Descendants

    * ants.core.ants_image.LabelImage

    ### Instance variables

    `direction`
    :   Get image direction
        
        Returns
        -------
        tuple

    `orientation`
    :

    `origin`
    :   Get image origin
        
        Returns
        -------
        tuple

    `spacing`
    :   Get image spacing
        
        Returns
        -------
        tuple

    ### Methods

    `abp_n4(image, intensity_truncation=(0.025, 0.975, 256), mask=None, usen3=False)`
    :

    `abs(self, axis=None)`
    :   Return absolute value of image

    `add_noise_to_image(image, noise_model, noise_parameters)`
    :

    `anti_alias(image)`
    :

    `apply(self, fn)`
    :   Apply an arbitrary function to ANTsImage.
        
        Args
        ----
        fn : python function or lambda
            function to apply to ENTIRE image at once
        
        Returns
        -------
        ANTsImage
            image with function applied to it

    `argmax(self, axis=None)`
    :   Return argmax along specified axis

    `argmin(self, axis=None)`
    :   Return argmin along specified axis

    `argrange(self, axis=None)`
    :   Return argrange along specified axis

    `as_label_image(self, label_info=None)`
    :

    `astype(self, dtype)`
    :   Cast & clone an ANTsImage to a given numpy datatype.
        
        Map:
            uint8   : unsigned char
            uint32  : unsigned int
            float32 : float
            float64 : double

    `clone(self, pixeltype=None)`
    :   Create a copy of the given ANTsImage with the same data and info, possibly with
        a different data type for the image data. Only supports casting to
        uint8 (unsigned char), uint32 (unsigned int), float32 (float), and float64 (double)
        
        Arguments
        ---------
        dtype: string (optional)
            if None, the dtype will be the same as the cloned ANTsImage. Otherwise,
            the data will be cast to this type. This can be a numpy type or an ITK
            type.
            Options:
                'unsigned char' or 'uint8',
                'unsigned int' or 'uint32',
                'float' or 'float32',
                'double' or 'float64'
        
        Returns
        -------
        ANTsImage

    `convolve_image(image, kernel_image, crop=True)`
    :

    `copy(self, pixeltype=None)`
    :   Create a copy of the given ANTsImage with the same data and info, possibly with
        a different data type for the image data. Only supports casting to
        uint8 (unsigned char), uint32 (unsigned int), float32 (float), and float64 (double)
        
        Arguments
        ---------
        dtype: string (optional)
            if None, the dtype will be the same as the cloned ANTsImage. Otherwise,
            the data will be cast to this type. This can be a numpy type or an ITK
            type.
            Options:
                'unsigned char' or 'uint8',
                'unsigned int' or 'uint32',
                'float' or 'float32',
                'double' or 'float64'
        
        Returns
        -------
        ANTsImage

    `create_tiled_mosaic(image, rgb=None, mask=None, overlay=None, output=None, alpha=1.0, direction=0, pad_or_crop=None, slices=None, flip_slice=None, permute_axes=False)`
    :

    `create_warped_grid(image, grid_step=10, grid_width=2, grid_directions=(True, True), fixed_reference_image=None, transform=None, foreground=1, background=0)`
    :

    `crop_image(image, label_image=None, label=1)`
    :

    `crop_indices(image, lowerind, upperind)`
    :

    `denoise_image(image, mask=None, shrink_factor=1, p=1, r=3, noise_model='Rician', v=0)`
    :

    `flatten(self)`
    :   Flatten image data

    `functional_lung_segmentation(image, mask=None, number_of_iterations=2, number_of_atropos_iterations=5, mrf_parameters='[0.7,2x2x2]', number_of_clusters=6, cluster_centers=None, bias_correction='n4', verbose=True)`
    :

    `fuzzy_spatial_cmeans_segmentation(image, mask=None, number_of_clusters=4, m=2, p=1, q=1, radius=2, max_number_of_iterations=20, convergence_threshold=0.02, verbose=False)`
    :

    `get_average_of_timeseries(image, idx=None)`
    :

    `get_center_of_mass(image)`
    :

    `get_centroids(image, clustparam=0)`
    :

    `get_mask(image, low_thresh=None, high_thresh=None, cleanup=2)`
    :

    `get_neighborhood_at_voxel(image, center, kernel, physical_coordinates=False)`
    :

    `get_neighborhood_in_mask(image, mask, radius, physical_coordinates=False, boundary_condition=None, spatial_info=False, get_gradient=False)`
    :

    `get_orientation(image)`
    :

    `get_pointer_string(image)`
    :

    `histogram_equalize_image(image, number_of_histogram_bins=256)`
    :

    `iMath(image, operation, *args)`
    :

    `iMath_GC(image, radius=1)`
    :

    `iMath_GD(image, radius=1)`
    :

    `iMath_GE(image, radius=1)`
    :

    `iMath_GO(image, radius=1)`
    :

    `iMath_MC(image, radius=1, value=1, shape=1, parametric=False, lines=3, thickness=1, include_center=False)`
    :

    `iMath_MD(image, radius=1, value=1, shape=1, parametric=False, lines=3, thickness=1, include_center=False)`
    :

    `iMath_ME(image, radius=1, value=1, shape=1, parametric=False, lines=3, thickness=1, include_center=False)`
    :

    `iMath_MO(image, radius=1, value=1, shape=1, parametric=False, lines=3, thickness=1, include_center=False)`
    :

    `iMath_canny(image, sigma, lower, upper)`
    :

    `iMath_fill_holes(image, hole_type=2)`
    :

    `iMath_get_largest_component(image, min_size=50)`
    :

    `iMath_grad(image, sigma=0.5, normalize=False)`
    :

    `iMath_histogram_equalization(image, alpha, beta)`
    :

    `iMath_laplacian(image, sigma=0.5, normalize=False)`
    :

    `iMath_maurer_distance(image, foreground=1)`
    :

    `iMath_normalize(image)`
    :

    `iMath_pad(image, padding)`
    :

    `iMath_perona_malik(image, conductance=0.25, n_iterations=1)`
    :

    `iMath_propagate_labels_through_mask(image, labels, stopping_value=100, propagation_method=0)`
    :

    `iMath_sharpen(image)`
    :

    `iMath_truncate_intensity(image, lower_q, upper_q, n_bins=64)`
    :

    `image_math(image, operation, *args)`
    :

    `image_to_cluster_images(image, min_cluster_size=50, min_thresh=1e-06, max_thresh=1)`
    :

    `kmeans_segmentation(image, k, kmask=None, mrf=0.1)`
    :

    `label_clusters(image, min_cluster_size=50, min_thresh=1e-06, max_thresh=1, fully_connected=False)`
    :

    `label_image_centroids(image, physical=False, convex=True, verbose=False)`
    :

    `label_stats(image, label_image)`
    :

    `labels_to_matrix(image, mask, target_labels=None, missing_val=nan)`
    :

    `list_to_ndimage(image, image_list)`
    :

    `mask_image(image, mask, level=1, binarize=False)`
    :

    `max(self, axis=None)`
    :   Return max along specified axis

    `mean(self, axis=None)`
    :   Return mean along specified axis

    `median(self, axis=None)`
    :   Return median along specified axis

    `min(self, axis=None)`
    :   Return min along specified axis

    `morphology(image, operation, radius, mtype='binary', value=1, shape='ball', radius_is_parametric=False, thickness=1, lines=3, include_center=False)`
    :

    `motion_correction(image, fixed=None, type_of_transform='BOLDRigid', mask=None, fdOffset=50, outprefix='', verbose=False, **kwargs)`
    :

    `movie(image, filename=None, writer=None, fps=30)`
    :

    `multi_label_morphology(image, operation, radius, dilation_mask=None, label_list=None, force=False)`
    :

    `n3_bias_field_correction(image, downsample_factor=3)`
    :

    `n3_bias_field_correction2(image, mask=None, rescale_intensities=False, shrink_factor=4, convergence={'iters': 50, 'tol': 1e-07}, spline_param=None, number_of_fitting_levels=4, return_bias_field=False, verbose=False, weight_mask=None)`
    :

    `n4_bias_field_correction(image, mask=None, rescale_intensities=False, shrink_factor=4, convergence={'iters': [50, 50, 50, 50], 'tol': 1e-07}, spline_param=None, return_bias_field=False, verbose=False, weight_mask=None)`
    :

    `ndimage_to_list(image)`
    :

    `new_image_like(self, data)`
    :   Create a new ANTsImage with the same header information, but with
        a new image array.
        
        Arguments
        ---------
        data : ndarray or py::capsule
            New array or pointer for the image.
            It must have the same shape as the current
            image data.
        
        Returns
        -------
        ANTsImage

    `nonzero(self)`
    :   Return non-zero indices of image

    `numpy(self, single_components=False)`
    :   Get a numpy array copy representing the underlying image data. Altering
        this ndarray will have NO effect on the underlying image data.
        
        Arguments
        ---------
        single_components : boolean (default is False)
            if True, keep the extra component dimension in returned array even
            if image only has one component (i.e. self.has_components == False)
        
        Returns
        -------
        ndarray

    `otsu_segmentation(image, k, mask=None)`
    :

    `pad_image(image, shape=None, pad_width=None, value=0.0, return_padvals=False)`
    :

    `plot(image, overlay=None, blend=False, alpha=1, cmap='Greys_r', overlay_cmap='turbo', overlay_alpha=0.9, vminol=None, vmaxol=None, cbar=False, cbar_length=0.8, cbar_dx=0.0, cbar_vertical=True, axis=0, nslices=12, slices=None, ncol=None, slice_buffer=None, black_bg=True, bg_thresh_quant=0.01, bg_val_quant=0.99, domain_image_map=None, crop=False, scale=False, reverse=False, title=None, title_fontsize=20, title_dx=0.0, title_dy=0.0, filename=None, dpi=500, figsize=1.5, reorient=True, resample=True)`
    :

    `plot_hist(image, threshold=0.0, fit_line=False, normfreq=True, title=None, grid=True, xlabel=None, ylabel=None, facecolor='green', alpha=0.75)`
    :

    `plot_ortho(image, overlay=None, reorient=True, blend=False, xyz=None, xyz_lines=True, xyz_color='red', xyz_alpha=0.6, xyz_linewidth=2, xyz_pad=5, orient_labels=True, alpha=1, cmap='Greys_r', overlay_cmap='jet', overlay_alpha=0.9, cbar=False, cbar_length=0.8, cbar_dx=0.0, cbar_vertical=True, black_bg=True, bg_thresh_quant=0.01, bg_val_quant=0.99, crop=False, scale=False, domain_image_map=None, title=None, titlefontsize=24, title_dx=0, title_dy=0, text=None, textfontsize=24, textfontcolor='white', text_dx=0, text_dy=0, filename=None, dpi=500, figsize=1.0, flat=False, transparent=True, resample=False, allow_xyz_change=True)`
    :

    `prior_based_segmentation(image, priors, mask, priorweight=0.25, mrf=0.1, iterations=25)`
    :

    `quantile(image, q, nonzero=True)`
    :

    `range(self, axis=None)`
    :   Return range tuple along specified axis

    `reflect_image(image, axis=None, tx=None, metric='mattes')`
    :

    `reorient_image2(image, orientation='RAS')`
    :

    `resample_image(image, resample_params, use_voxels=False, interp_type=1)`
    :

    `resample_image_to_target(image, target, interp_type='linear', imagetype=0, verbose=False, **kwargs)`
    :

    `rgb_to_vector(image)`
    :

    `scalar_to_rgb(image, mask=None, filename=None, cmap='red', custom_colormap_file=None, min_input=None, max_input=None, min_rgb_output=None, max_rgb_output=None, vtk_lookup_table=None)`
    :

    `set_direction(self, new_direction)`
    :   Set image direction
        
        Arguments
        ---------
        new_direction : numpy.ndarray or tuple or list
            updated direction for the image.
            should have one value for each dimension
        
        Returns
        -------
        None

    `set_origin(self, new_origin)`
    :   Set image origin
        
        Arguments
        ---------
        new_origin : tuple or list
            updated origin for the image.
            should have one value for each dimension
        
        Returns
        -------
        None

    `set_spacing(self, new_spacing)`
    :   Set image spacing
        
        Arguments
        ---------
        new_spacing : tuple or list
            updated spacing for the image.
            should have one value for each dimension
        
        Returns
        -------
        None

    `slice_image(image, axis, idx, collapse_strategy=0)`
    :

    `smooth_image(image, sigma, sigma_in_physical_coordinates=True, FWHM=False, max_kernel_width=32)`
    :

    `split_channels(image)`
    :

    `std(self, axis=None)`
    :   Return std along specified axis

    `sum(self, axis=None, keepdims=False)`
    :   Return sum along specified axis

    `symmetrize_image(image)`
    :

    `threshold_image(image, low_thresh=None, high_thresh=None, inval=1, outval=0, binary=True)`
    :

    `to_file(self, filename)`
    :   Write the ANTsImage to file
        
        Args
        ----
        filename : string
            filepath to which the image will be written

    `to_filename(self, filename)`
    :   Write the ANTsImage to file
        
        Args
        ----
        filename : string
            filepath to which the image will be written

    `to_nibabel(image)`
    :

    `unique(self, sort=False)`
    :   Return unique set of values in image

    `vector_to_rgb(image)`
    :

    `view(self, single_components=False)`
    :   Geet a numpy array providing direct, shared access to the image data.
        IMPORTANT: If you alter the view, then the underlying image data
        will also be altered.
        
        Arguments
        ---------
        single_components : boolean (default is False)
            if True, keep the extra component dimension in returned array even
            if image only has one component (i.e. self.has_components == False)
        
        Returns
        -------
        ndarray

    `weingarten_image_curvature(image, sigma=1.0, opt='mean')`
    :

`LabelImage(label_image, label_info=None, template=None)`
:   A LabelImage is a special class of ANTsImage which has discrete values
    and string labels or other metadata (e.g. another string label such as the
    "lobe" of the region) associated with each of the discrete values.
    A canonical example of a LabelImage is a brain label_image or parcellation.
    
    This class provides convenient functionality for manipulating and visualizing
    images where you have real values associated with aggregated image regions (e.g.
    if you have cortical thickness values associated with brain regions)
    
    Commonly-used functionality for LabelImage types:
        - create publication-quality figures of an label_image
    
    Nomenclature
    ------------
    - key : a string representing the name of the associated index in the atlas image
        - e.g. if the index is 1001 and the key may be InferiorTemporalGyrus`
    - value : an integer value in the atlas image
    - metakey : a string representing one of the possible sets of label key
        - e.g. 'Lobes' or 'Regions'
    Notes
    -----
    - indexing works by creating a separate dict for each metakey, where
    
    Initialize a LabelImage
    
    ANTsR function: N/A
    
    Arguments
    ---------
    label_image : ANTsImage
        discrete (integer) image as label_image
    
    label_info : dict or pandas.DataFrame
        mapping between discrete values in `image` and string names
        - if dict, the keys should be the discrete integer label values
          and the values should be the label names or another dict with
          any metadata
        - if pd.DataFrame, the index (df.index) should be the discrete integer
          label values and the other column(s) should be the label names and
          any metadata
    
    template : ANTsImage
        default real-valued image to use for plotting or creating new images.
        This image should be in the same space as the `label_image` image and the
        two should be aligned.
    
    Example
    -------
    >>> import ants
    >>> square = np.zeros((20,20))
    >>> square[:10,:10] = 0
    >>> square[:10,10:] = 1
    >>> square[10:,:10] = 2
    >>> square[10:,10:] = 3
    >>> img = ants.from_numpy(square).astype('uint8')
    >>> label_image = ants.LabelImage(label_image=img, label_info=label_dict)

    ### Ancestors (in MRO)

    * ants.core.ants_image.ANTsImage

    ### Methods

    `generate_data(self)`
    :

    `items(self, metakey)`
    :

    `keys(self, metakey=None)`
    :

    `metakeys(self)`
    :

    `n_values(self)`
    :

    `parentkey(self, key)`
    :

    `uniquekeys(self, metakey=None)`
    :   Get keys for a given metakey

    `values(self)`
    :