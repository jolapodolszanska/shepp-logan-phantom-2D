### Shepp-Logan phantom

Shepp-Logan phantom is is a standard test image created by Larry Shepp and Benjamin F. Logan for their 1974 paper The Fourier Reconstruction of a Head Section.It serves as the model of a human head in the development and testing of image reconstruction algorithms[1].



I know how difficult it is to implement this model, which is why I present the simplest solution. My model was created by values of the table:

|Ellipse  | Center         |  Major Axis  | Minor Axis  | Theta | Gray level  |
| --------| ---------------|--------------|-------------|-------|-------------|
| I       | (0,0)          |  0.69        | 0.92        | 0     | 2           |
| II      | (0,−0.0184)    |  0.6624      | 0.874       | 0     | −0.98       |
| III     |  	(0.22,0)     |  0.11        | 0.31        | −18°  | −0.02       |
| IV      | (−0.22,0)      |  0.16        | 0.41        | 18°   | −0.02       |
| V       | (0,0.35)       |  0.21        | 0.25        | 0     | 0.01        |
| VI      | (0,0.1)        |  0.046       | 0.046       | 0     | 0.01        |
| VII     | (0,−0.1)       |  0.046       | 0.046       | 0     | 0.01        |
| VIII    | (−0.08,−0.605) |  0.046       | 0.023       | 0     | 0.01        |
| IX      | (0,−0.605)     |  0.023       | 0.023       | 0     | 0.01        |
| X       | (0.06,−0.605)  |  0.023       | 0.046       | 0     | 0.01        |

Result of running application:

<img src="https://raw.githubusercontent.com/jolapodolszanska/shepp-loganphan-phantom-2D/main/pobrane.png" />

### Parallel Beam CT 

We began by creating an image using a thoracic Shepp-Logan phantom. Several tuning parameters were added to simulate object movement (shifting). Projections are created through line integrals (summations) between two points anywhere inside and/or outside the image. Details can be found in the Thoracic Cavity Phantom section of the report. For a given angle, a projection consists of a vector of parallel line integrals formed by a source on one side of the image and a line of detectors on the other. The size of the projection vector is equal to the number of detectors in the array. Thus, a ten detector projection will have ten line integral summations. The detectors can be spaced apart at various widths depending on the array length. Thus, an array of length two with ten detectors will have twice the spacing between detectors as an array of length one with ten detectors. We compute these projections for various uniform angle spacing between 0 and 180 degrees.

Many different images were obtained for various array lengths, detector quantities, and angle resolutions. The squared error between the reconstructed image and the original were computed as a metric to judge reconstruction quality. Furthermore, we tried to reduce the squared error through image enhancement. Some filters included adaptive Wiener FIR filters, median filters, and high pass filters[1]

Let's see geometry and model[3]
<img src="https://raw.githubusercontent.com/jolapodolszanska/shepp-loganphan-phantom-2D/main/Tomography-with-parallel-beam-geometry-The-left-image-shows-the-geometry-of-a-typical_W640.jpg" />

### References
[1] Shepp, Larry A.; Logan, Benjamin F. (June 1974). "The Fourier Reconstruction of a Head Section" (PDF). IEEE Transactions on Nuclear Science. NS-21 (3): 21–43
[2] Robert Cierniak, X-Ray Computed Tomography in Biomedical Engineering, 2011, Springer, ISBN : 978-0-85729-026-7
[3] Bleichrodt, F., van Leeuwen, T., Palenstijn, W.J. et al. Easy implementation of advanced tomography algorithms using the ASTRA toolbox with Spot operators. Numer Algor 71, 673–697 (2016). https://doi.org/10.1007/s11075-015-0016-4
