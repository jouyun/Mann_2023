# Mann_2023

Image analysis code associated with the submitted publication of Blair Benham-Pyle and Frederick Mann.  

SegmentNucleiiAndQuantify_porcna_archive.ipynb and SegmentNucleiiAndQuantify_mmp1_archive.ipynb take a series of spinning disk confocal z-stacks that have been exported from Fiji (after background subtraction) and processes them in 3 stages:

1.  Projecting 1um stacks to a smaller series of 6um stacks, where the non-DAPI channels have been maximally projected in order to collect all potential signal from one cell into a single image and the DAPI has had only the middle two sections maximally projected.  Projecting the entire DAPI over this range had negative effects on the results from Cellpose.  Segmentation is then run on the projected DAPI channels using the 'cyto' model from Cellpose with a diameter of 50 pixels.  Results are written out with a similar filename.
2.  Quantifying of the nuclear labels is performed, measuring the integrated signal intensities for all channels in the regions defined by the nuclear labels.  For mmp1, the mmp1 channel is thresholded and a Euclidian Distance Transform calculated for performing distance measurements later.  The output of this stage is a pandas dataframe with each nucleus having its own entry and quantification.
3.  Signal intensities for each nucleus are normalized by finding the 30th percentile of intensities for each channel/slice/file and dividing all intensities at the same channel/slice/file by that value.  This accounts for signal attenuation at different penetration depths and for animal-to-animal variability.  A threshold is then selected based on visual inspection and then applied to determine which nucleii are positive for the various labels.

Remaining code is for visualization and statistical analysis of the results.
