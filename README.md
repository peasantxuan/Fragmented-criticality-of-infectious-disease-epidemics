# Fragmented criticality of infectious disease epidemics

This small research repository accompanies the paper *Fragmented criticality of infectious disease epidemics*.

Fragmented criticality describes how population structure can turn the individual thresholds of weakly coupled strata into complex-valued critical points. Their real parts locate critical changes along the transmissibility axis, their imaginary parts quantify smearing, and their critical modes identify the strata involved. The method uses a structured reproduction operator `R = r C`.

The repository revolves around two notebooks:

- `numerical_method.ipynb` contains the reusable numerical method: epidemic probabilities, the extinction-conditioned operator, expected minor-outbreak sizes, complex critical points, and localized modes. Its Figure 1 two-stratum example (`C = [[0.5, 0], [0.006, 1]]`) is fully reproducible without empirical data.
- `analysis.ipynb` organizes the Italy, Texas, LA-MRSA, vaccination, and figure-generation analyses. Empirical sections run only when their documented inputs are present.

Meta Colocation Maps used for Italy and Texas cannot be redistributed. See `data/README.md` for sources, expected formats, and placement. No restricted mobility files are included.

To use the method with another population, replace `C` in `numerical_method.ipynb` with any non-negative square matrix that follows the documented convention (and normalize it if desired).

## Run

```bash
python -m pip install -r requirements.txt
jupyter notebook numerical_method.ipynb
```

For the empirical workflow, supply authorized inputs first and run:

```bash
jupyter notebook analysis.ipynb
```
