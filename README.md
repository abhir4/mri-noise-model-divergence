# MRI Noise Model Divergence: Rician vs. Gaussian Across Field Strength

**Does the type of noise model chosen change observations about optimal MRI field strength?**

This project simulates T1 wieghted MRI images across a range of magnetic field strengths using to different noise models viz. Gaussian and Rician. We also compare how each noise model affects the image quality from which we draw our conclusions.

TLDR: There is a bit of divergence which is not constant across the spectrum of magnetic fields. 

**Real MRI images have Rician distribution and not Gaussian**
Despite that, Gaussian is still a common simplifying assumption to simulate and benchmark since it is easier to reason and simulate. The aim of this project is to explore the effect of this simplification. We consider the choice of noise model as an experimental variable along with field strength rather than a fixed assumption.

## Method

- **Base Data:** Discrete anatomical labeled volumes (GM, WM, CSF) used to build synthetic T1 weighted signals using analytical signal equation with realistic T1, T2* values, TE, TR, bandwidth, flip angle.
- **Noise:** Each slice that is simulated is added with Gaussian or Rician noise at a calibrated SNR with Rayleigh bias correction so that we can compare on a similar level vs using an image that is noisier from the start.
- **Sweep:** We simulate the images fully, then add noise, measure the difference across a range of magnetic field strengths, with multiple noise realizations averaged at each point to reduce single draw noise while comparing.
- **Metrics:** At each field strength, the SNR, gradient entropy, and edge sharpness was measured to see the nature of noise models.

- ## Repo structure
 
```
├── project1.ipynb          # Full analysis notebook (run top to bottom)
├── requirements.txt        # Pinned package versions
├── DATA.md                 # How to source and set up the input data
├── LICENSE                 # MIT
└── README.md
```

1. Clone the repo and install dependencies:
```bash
   pip install -r requirements.txt
```
2. Set up the input data — see [`DATA.md`](DATA.md) for the expected
   format and directory layout. The data itself is not included in this
   repo (see below).
3. Open `project1.ipynb` and run all cells. The main output figures are
   saved automatically as the notebook runs.

   ## A note on the data
 
The anatomical label volumes used here are BrainWeb style digital phantom
data and are not redistributed in this repo. `DATA.md` explains the
expected format and where to source equivalent data if you want to
reproduce or extend this work.

## Origin
 
This project began as an extension of coursework in medical imaging,
built around the same analytical signal-simulation approach used there,
then extended into a standalone noise-model comparison.
 
## License
 
MIT — see [`LICENSE`](LICENSE). Note this covers the code only; it does
not grant any rights to the input MRI data, which is sourced separately
(see `DATA.md`).
