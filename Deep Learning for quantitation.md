The basic dataset is **uniform-22.5k** which features *22500* brain spectra were simulated using actual RF pulse shapes for 3T and 16 metabolites using Vespa for a semi-LASER protocol with TE=35ms, a sampling frequency of 4kHz and 4096 datapoints. A constant downscaled water reference (64.5mM) is added at 0.5ppm to ease quantitation.

- metabolite concentration range vary from dataset to dataset. Basic dataset uniform-22.5k reports metabolite concentrations that vary independently and uniformly between 0 and twice a normal reference concentration for healthy human brain. Maximal concentrations in mM units: NAA (N-acetylaspartic acid) 25.8, tCr (1:1 sum of creatine + phosphocreatine spectra): 18.5, mI (myo-inositol): 14.7, Glu (glutamate): 20, Glc (glucose): 2, NAAG (N-acetylaspartylglutamate): 2.8, Gln (glutamine): 5.8, GSH (glutathione): 2, sI (syllo-inositol): 0.6, Gly (glycine): 2, Asp (aspartate): 3.5, PE (phosphoethanolamine): 3.3, Tau (taurine): 2, Lac (lactate): 1, GABA (γ-aminobutyric acid): 1.8. The concentration for tCho (1:1 sum of glycerophosphorylcholine + phosphorylcholine spectra) ranges from 0 to 5mM to mimic tumor conditions. 
- metabolite T2s in ms (and hence Lorentzian broadening) are fixed to reference values from literature: tCr (CH2): 111, tCr (CH3): 169, NAA (CH3): 289, all other protons: 185.49
- MMBG content, shim, and SNR mimicked in vivo acquisitions and varied independently and uniformly (time-domain water referenced SNR 5-40, Gaussian shim 2-5 Hz, MMBG amplitude ±33%). The MMBG pattern was simulated as a sum of overlapping Voigt lines.


**uniform-20k**: 

  *training set* (20000 entries):
  
    - dataset_spectra.mat: 20000x1024 complex domain spectra, [# samples, chemical shift]
    - dataset_spectra_gt.mat: 20000x1024 complex domain spectra ground truth (i.e., no MMBG, no shim), [# samples, chemical shift]
    - dataset_spgram.mat: 20000x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part]
    - dataset_spgram_gt.mat: 20000x128x32x2 spectrogram ground truth (i.e., no MMBG, no shim), [# samples, chemical shift bins, time bins, real and imaginary part]
    - labels_c.mat: 20000x16 relative to water concentration values, [# samples, metabolites]
  
  *test set* (2500 entries):
  
    - dataset_spectra_TEST.mat: 2500x1024 complex domain spectra, [# samples, chemical shift]
    - dataset_spgram_TEST.mat: 2500x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part]
    - labels_c_TEST.mat: 2500x16 relative to water concentration values, [# samples, metabolites]
    - shim_v_TEST.mat: 2500x1 shim values in Hz, [# samples, ]
    - snr_v_TEST.mat: 2500x1 time domain SNR, [# samples, ]
    
 **uniform-20k-v2**: 
 
 complete new simulation with identical parameters from **uniform-20k** which saves and extends the results with and without water reference peak and with chemical shift and number of data points that allow processing to U-Net architectures. 
 
  *training set* (20000 entries):
  
    - dataset_spectra.mat: 20000x1024 complex domain spectra, [# samples, chemical shift]
    - dataset_spectra_nw.mat: 20000x1024 complex domain spectra, [# samples, chemical shift] *nw*: no water reference
    - dataset_spectra_unet.mat: 20000x1356 real domain spectra, [# samples, chemical shift]
    - dataset_spectra_unet_nw.mat: 20000x1356 real domain spectra, [# samples, chemical shift] *nw*: no water reference
    - dataset_spgram.mat: 20000x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part]
    - dataset_spgram_nw.mat: 20000x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part] *nw*: no water reference
    - labels_c.mat: 20000x16 relative to water concentration values, [# samples, metabolites]
    - labels_c_nw.mat: 20000x16 relative to water concentration values, [# samples, metabolites] *nw*: no water reference
    - labels_s_mXX_nw: 20000x1356 real domain spectra of basis set (i.e., no MMBG, no shim) of metabolite XX, [# samples, chemical shift]. XX goes from 01 to 17 (1:tCho, 2:NAAG, 3:NAA, 4:Asp, 5:tCr, 6:GABA, 7:Glc, 8:Glu, 9:Gln, 10:GSH, 11:Gly, 12:Lac, 13:mI, 14:PE, 15:sI, 16:Tau, 17:Water.
  
  *test set* (2500 entries):
 
    - dataset_spectra_TEST.mat: 2500x1024 complex domain spectra, [# samples, chemical shift]
    - dataset_spectra_nw_TEST.mat: 2500x1024 complex domain spectra, [# samples, chemical shift] *nw*: no water reference
    - dataset_spectra_unet_TEST.mat: 2500x1356 real domain spectra, [# samples, chemical shift]
    - dataset_spectra_unet_nw_TEST.mat: 2500x1356 real domain spectra, [# samples, chemical shift] *nw*: no water reference
    - dataset_spgram_TEST.mat: 2500x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part]
    - dataset_spgram_nw_TEST.mat: 2500x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part] *nw*: no water reference
    - labels_c_TEST.mat: 2500x16 relative to water concentration values, [# samples, metabolites]
    - labels_c_nw_TEST.mat: 2500x16 relative to water concentration values, [# samples, metabolites] *nw*: no water reference
    - labels_s_mXX_nw_TEST: 2500x1356 real domain spectra of basis set (i.e., no MMBG, no shim) of metabolite XX, [# samples, chemical shift]. XX goes from 01 to 17 (1:tCho, 2:NAAG, 3:NAA, 4:Asp, 5:tCr, 6:GABA, 7:Glc, 8:Glu, 9:Gln, 10:GSH, 11:Gly, 12:Lac, 13:mI, 14:PE, 15:sI, 16:Tau, 17:Water.
    - shim_v_TEST.mat: 2500x1 shim values in Hz, [# samples, ]
    - snr_v_TEST.mat: 2500x1 time domain SNR, [# samples, ]  
    
## active_learning_training_sets:
The following dataset models variation from uniform-20k which are used for active learning purposes in training phase. 

**uniform-40k**: 

identical to uniform-20k training set extended with further 20k entries:

- dataset_spgram.mat: 40000x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part]
- dataset_spectra.mat: 40000x1024 spectra, [# samples, chemical shift bins]
- labels_c.mat: 40000x16 relative to water concentration values, [# samples, metabolites]

**uniform-25k**: 

identical to uniform-20k training set extended with further 5000 entries:
  - dataset_spgram.mat: 25000x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part]
  - labels_c.mat: 25000x16 relative to water concentration values, [# samples, metabolites]
  *ns*: folder that contains the added 5000 simulations only. It reports:  
    - dataset_spectra: 2500x1024 complex domain spectra, [# samples, chemical shift]
    - dataset_spectra_gt: 2500x1024 complex domain spectra ground truth (i.e., no MMBG, no shim), [# samples, chemical shift]
    - dataset_spgram: 2500x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part]
    - dataset_spgram_gt: 2500x128x32x2 spectrogram,ground truth (i.e., no MMBG, no shim), [# samples, chemical shift bins, time bins, real and imaginary part]
    - labels_c: 2500x16 relative to water concentration values, [# samples, metabolites]

**fully-w**: 

identical to uniform-20k training set extended with further 5000 entries with concentration in 0-20% and 80-100% range (2500 entries per category, uniformily  distributed in the interval) for all metabolites. *Similar nested structure to uniform-25k*.

**GABA-w**: 

identical to uniform-20k training set extended with further 5000 entries with concentration in 0-20% and 80-100% range (2500 entries per category, uniformily  distributed in the interval) for GABA only. *Similar nested structure to uniform-25k*.
  
**sI-w**: 

identical to uniform-20k training set extended with further 5000 entries with concentration in 0-20% and 80-100% range (2500 entries per category, uniformily  distributed in the interval) for sI only. *Similar nested structure to uniform-25k*.
  
**GSPT-w**: 

identical to uniform-20k training set extended with further 5000 entries with concentration in 0-20% and 80-100% range (2500 entries per category, uniformily  distributed in the interval) for GABA, sI, PE and Tau (i.e., GSPT) only. *Similar nested structure to uniform-25k*.
  
**SNR-w**: 

identical to uniform-20k training set extended with further 5000 entries with uniform concentrations but low SNR (time domain SNR between 5-15). *Similar nested structure to uniform-25k*.

## active_learning_testsets:
The following dataset models variation from uniform-22.5k test set which are used for active learning purposes in testing phase. 

  - *_0mu*: concentration range for all metabolites is uniformily distributed but restricted from 0 to the average value (from dataset uniform-22.5k).
  - *_0208*: concentration range for all metabolites is uniformily distributed but but restricted from 20% to 80% the original range (i.e., dataset uniform-22.5k). 
  - *_0406*: concentration range for all metabolites is uniformily distributed but restricted from from 40% to 60% the original range (i.e., dataset uniform-22.5k).
  - *_0208_hSNR*: concentration range for all metabolites is uniformily distributed but restricted from 20% to 80% the original range (i.e., dataset uniform-22.5k) and entries are simulated only with high SNR.
  
  each folder contains (*_XX* stands for the folder parents' name):
    - dataset_spgram_TEST_XX.mat: 2500x128x32x2 spectrogram, [# samples, chemical shift bins, time bins, real and imaginary part]
    - labels_c_TEST_XX.mat: 2500x16 relative to water concentration values, [# samples, metabolites]
    - shim_v_TEST_XX.mat: 2500x1 shim values in Hz, [# samples, ]
    - snr_v_TEST_XX.mat: 2500x1 time domain SNR, [# samples, ]
