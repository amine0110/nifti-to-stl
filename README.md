# Convert Nifti Files into STL Files

This code is for converting the 3D segmentation files (Nifti) into 3D mesh representation (STL). If you are interested about the project then you can read more in this [article](https://pycad.co/nifti-to-stl/).

The operation is very easy and can be done if a few lines of code.

```Python
import nibabel as nib
import numpy as np
from stl import mesh
from skimage import measure

# Path to the nifti file (.nii, .nii.gz)
file_path = 'segmentation.nii'

# Extract the numpy array
nifti_file = nib.load(file_path)
np_array = nifti_file.get_fdata()

verts, faces, normals, values = measure.marching_cubes(np_array, 0)
obj_3d = mesh.Mesh(np.zeros(faces.shape[0], dtype=mesh.Mesh.dtype))

for i, f in enumerate(faces):
    obj_3d.vectors[i] = verts[f]

# Save the STL file with the name and the path
obj_3d.save('segmentation.stl')
```


<p align="center">
  <img src="https://user-images.githubusercontent.com/37108394/198897186-21ac8495-a5e1-47f0-b476-f1b5b3995659.gif" />
</p>

## 🆕NEW
Learn how to effectively manage and process DICOM files in Python with our comprehensive course, designed to equip you with the skills and knowledge you need to succeed.

https://www.learn.pycad.co/course/dicom-simplified
