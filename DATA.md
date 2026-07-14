# Data setup
This project runs on two BrainWeb style discrete anatomical label volumes
(one per simulated patient). The volumes are **not included in this repo**,
you'll need to source them yourself and point the notebook at them.

## Data format expectations

Each volume is a 3D NIfTI file (`.nii`) containing an integer label map, not
a raw MR image. Label values used by `extract_tissue_masks()`:

| Label value | Tissue        |
|-------------|---------------|
| 0           | Background    |
| 1 or 2      | Grey matter   |
| 3           | White matter  |
| 4           | CSF           |

The notebook loads a single axial slice (`SLICE_IDX`, default 90) out of
the full 3D volume and simulates signal/noise on top of it.  We do not
need the whole volume in memory beyond that.

## Getting the data

These specific volumes were provided directly by a course instructor rather
than downloaded by us, so we can't give an exact download link that's
guaranteed to reproduce them. If you don't already have
equivalent files. Any BrainWeb derived label volume in that format should work as a drop in
replacement. Additionally, the code only depends on the label values of the volume.

## Directory layout

Set the `MRI_DATA_DIR` environment variable to the folder containing your
data, then lay it out like this:

$MRI_DATA_DIR/
├── Patient1.nii/
│   └── Patient1.nii
└── Patient2.nii/
    └── Patient2.nii

(Data files were packaged with the same name as their folders and hence they appear with the same name)

If `MRI_DATA_DIR` isn't set, the notebook defaults to `./data` relative to
wherever you run it from.

### Setting the environment variable

**Locally / any Jupyter server:**
export MRI_DATA_DIR=/path/to/your/data
jupyter notebook

**Google Colab:**
import os
os.environ["MRI_DATA_DIR"] = "/content/drive/MyDrive/MRI_PROJECT_DATA"
(mount your own Drive with the data placed as per tha bove layout)

## Test

Once `MRI_DATA_DIR` is set and the files are in place, the very first
cell in the notebook (tissue mask extraction) will display a 2x2 panel -
the raw label slice plus its GM, WM, and CSF masks for Patient 1.
