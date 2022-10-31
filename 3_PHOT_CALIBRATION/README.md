# Photometric Calibration
These Jupyter Notebook calculate the Photometric Calibration data needed to fix catalog's magnitudes. The data we're going to calculate are the atmospheric Extinction Coefficient $k$, the Photometric Zero-Point $ZP$ and the random background fluctuations $\sigma_b$.

## Atmospheric Extinction Coefficient $k$
The extinction coefficient is different for each filter. To calculate $k$ we need to work with the single individual exposures to measure the magnitude differences along the airmass variance during the night.

1. Find the airmass $X$ for each exposure.
2. Measure the magnitud for the same star in all the exposures.
3. Plot tha star magnitude versus the airmass.
4. Fit a linear regression to the data.
5. The slope of the fit corresponds to the extinction coefficient $k$.

Now, the magnitude is defined as:

$m_{atm}=m_{sex}-kX$

where $m_{atm}$ is the magnitude above the atmosphere, $m_{sex}$ is the instrumental mangitude mesaured by SEXtractor and $kX$ is the atmospheric calibration.

## Photometric Zero-Point $ZP$
We have to transform our magnitudes into and standard model magnitudes, the AB system. To do that, we'll calculate the $ZP$ of our filters.

1. Download literature catalogues of our objects. For filters $grizY$ we use the Dark Energy Survey Data Release II. For filter $u$ we use the Guide Star Catalogue.
2. Crossmatch our SEXtractor catalogues with the literature catalogs, considering only stars brighter than 18 $mag$.
3. Calculate the $ZP$ with the formula:

    $ZP=m_{cat}-m_{atm}$
    
    where $m_{cat}$ is the catalog magnitude.
    
4. Then, we calculate the median, mean, standard deviation and photometric error. The final $ZP$ will be the median of the sample obtained, and the photometric arror associated is given by:

    $\Delta ZP=\sqrt{(\Delta m_{cat}+\Delta m_{atm})^2+\sigma_{ZP}^2}$
    
    where $\Delta m_{cat}$ and $\Delta m_{atm}$ are the photometric errors of the catalog and SEXtractor magnitude respectively.
    
Finally, the AB magnitude of an object is given by:

  $m_{AB}=m_{cat}+ZP$
  
## Random Background Fluctuations $\sigma_b$
This is a way to measure the noise produced by the sky background in our images, and is important to the photometric error estimation and for the signal-to-noise ratio calculation.

1. Set $n$ apertures with radius $r$ in the sky background of the image. $n$ and $r$ are arbitrary, so in our case, we're going to set $n=120$ apertures with $r=10''$ radius.
2. Measure the flux inside the apertures.
3. Calculate the RMS of the fluxes. This RMS is $\sigma_b$.

## Final magnitude
After all the calibrations and error estimations, the definitive magniutde for an object is given by:

$m\pm\Delta m=(m_{sex}-kX+ZP)\pm\sqrt{\Delta m_{sex}^2+\Delta ZP^2+\sigma_b^2}$
