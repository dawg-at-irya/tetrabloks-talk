# Presentation about Tetrabloks algorithm

Will Henney - DAWGI Meeting - 2019 June 24

## Animation ##

![Animated GIF of presentation](presentation/dawgi-tetrabloks-presentation.gif)

## Individual slides ##

### Title page ###

![Tetrabloks - an algorithm for multi-resolution mapping of inhomogeneous data](slides/tb.001.jpeg)

### Inhomogeneous data ###

Tetrabloks is an algorithm for making maps of inhomogeneous data.
Different use cases for the algorithm include:

1. Missing pixels: Tetrabloks will interpolate these regions away, even if they are large
2. Noisy regions: Tetrabloks can smooth out high-noise regions while preserving the spatial resolution of low-noise regions
3. Sparse and non-uniform spatial coverage: Tetrabloks can produce maps from an arbitrary set of points. It works well for combining multiple slit positions and orientations of longslit spectroscopy. 

![Inhomogeneous data](slides/tb.002.jpeg "Inhomogeneous data")

### Multi-resolution ###
Multi-resolution mapping proceeds via two steps. 

The first step is binning: each 2x2 block of pixels is averaged to give the next-coarser grid. Each pixel may have an associated weight, which is used in the averaging. A weight of zero indicates a missing or bad pixel (red in the figures), which does not contribute to the coarse grid. A tuneable parameter `mingood` specifies the minimum number of good pixels that a 2x2 block must have in order to create a good pixel on the coarse grid. A value of `mingood = 1` (the default) means that good regions "bleed" into bad regions, causing the bad regions to shrink. The binning is repeated to produce a sequence of coarser and coarser grids: 1x1, 2x2, 4x4, 8x8, etc.

![Multi-resolution: step 1](slides/tb.003.jpeg "Multi-resolution: step 1")

The second step is stack the sequence of grid. In the simplest version (as illustrated), each pixel comes from the finest grid  where it has a non-zero weight. Alternatively, other criteria can be used, such as a minimum signal/noise ratio.

![Multi-resolution: step 2](slides/tb.004.jpeg "Multi-resolution: step 2")

### Application I - noisy image ###

Before.

![Application I: before](slides/tb.005.jpeg "Application I: before")

After.

![Application I: after](slides/tb.006.jpeg "Application I: after")

### Application II - noisy ratio ###

Individual binning levels. 

![Application II: 1x1](slides/tb.007.jpeg "Application II: 1x1")
![Application II: 4x4](slides/tb.008.jpeg "Application II: 4x4")
![Application II: 16x16](slides/tb.009.jpeg "Application II: 16x16")
![Application II: 64x64](slides/tb.010.jpeg "Application II: 64x64")

Fixed signal-to-noise of the density.

![Application II: S/N=10](slides/tb.011.jpeg "Application II: S/N=10")
![Application II: S/N=100](slides/tb.012.jpeg "Application II: S/N=100")

### Application III - slit spectra ###

![Application III: original slits](slides/tb.013.jpeg "Application III: original slits")
![Application III: multibinning](slides/tb.014.jpeg "Application III: multibinning")
![Application III: high velocities](slides/tb.015.jpeg "Application III: high velocities")

### Tetrapak + Megabloks = Tetrabloks ###

Inspiration for the name.

![Tetrapak + Megabloks = Tetrabloks](slides/tb.016.jpeg "Tetrapak + Megabloks = Tetrabloks")

