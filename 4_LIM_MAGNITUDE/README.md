# Limit Magnitudes Notebook
The jupyter notebook calculates the limit magnitud of the photometric catalogues produced by SEXtractor. This notebook also performs photometric calibration for all the objects in the catalogues.

The procedure is as follows:

1. Apply photometric calibration to the detected objects.
2. Calculate "Signal-to-Noise" ratio to all the objects:

    $\displaystyle\frac{S}{N}=\displaystyle\frac{F}{\sqrt{F+\sigma_b^2}}$
      
    where $F$ is the object flux in a r=10'' aperture and $\sigma_b$ are the random background fluctuations measured in r=10'' apertures:
      
3. Delete all the objectos with $\frac{S}{N}<5$.
4. Make histograms of object's magnitudes. In this case we use the SEXtractor automathic magnitude MAG_AUTO.
5. Calculate the peak of the histogram (the magnitude's mode). This peak corresponds, 'a priori', to the limit magnitude of the catalog.
