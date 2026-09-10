# Fragmented criticality of infectious disease epidemics

This small research repository accompanies the paper *Fragmented criticality of infectious disease epidemics*. It is organized around two notebooks and is not a software package.

## Theory in brief

Consider a multitype Galton–Watson process with population strata (i=1,\ldots,N). If (X_{i\to j}) is the number of secondary infections generated in stratum (j) by an infected individual from stratum (i), the matrix convention is

\[
\mathbb{E}[X_{i\to j}] = R_{ji}, \qquad \mathbf R=r\mathbf C,
\]

where (\mathbf C\) is non-negative and normalized to spectral radius one, and (r>0) is the reference reproduction ratio. With independent Poisson offspring, the major-epidemic probabilities satisfy

\[
F_i(\mathbf p,r)=p_i-1+\exp\!\left(-r\sum_j C_{ji}p_j\right)=0.
\]

Conditioning on eventual extinction gives the tilted reproduction operator

\[
\widehat R_{ij}=(1-p_i)R_{ij},
\]

and the expected size of a minor outbreak is

\[
\overline{\mathbf Y}=(\mathbf I-\widehat{\mathbf R}^{\mathsf T})^{-1}\mathbf 1.
\]

The ordinary epidemic threshold is the positive real value at which this resolvent is singular. In a structured population, the other stratum-level singularities generally move into the complex (r)-plane. These are the **fragmented critical points**. For a point (r_c), (\operatorname{Re}r_c) locates the associated change in transmissibility, |(\operatorname{Im}r_c)| controls its strength and smearing, and the near-null right eigenvector of

\[
\mathbf L=\mathbf I-\mathbf U,\qquad U_{ij}=(1-p_i)R_{ji},
\]

identifies the involved strata. Mode localization is reported as (\widetilde w_i=|w_i|/\sqrt{\sum_j|w_j|^2}). Near a simple critical point, the minor-outbreak response has the resonance-like form

\[
\overline{\mathbf Y}\propto
\frac{\mathbf w}{\sqrt{(r-\operatorname{Re}r_c)^2+(\operatorname{Im}r_c)^2}}.
\]

Thus epidemic emergence is described by a critical landscape—when, how sharply, and in which subpopulations vulnerability appears—rather than only by one system-wide threshold.

## Notebooks

- `numerical_method.ipynb` contains the reusable calculation: epidemic probabilities, extinction conditioning, expected minor-outbreak sizes, complex critical points, and localized critical modes. Its Figure 1 demonstration uses (C=\begin{pmatrix}0.5&0\\0.006&1\end{pmatrix}) and requires no empirical data.
- `analysis.ipynb` organizes the Italy, Texas, LA-MRSA, vaccination, and figure-generation analyses. It reuses the numerical functions without introducing a package or a collection of modules.

To apply the method elsewhere, replace `C` in `numerical_method.ipynb` with any non-negative square mixing/reproduction matrix using the convention above.

## Data

Small public inputs used by the empirical analyses are included under `data/`, together with source snapshots where useful:

- Italian province populations and the modeled 2010 global air-passenger flows of [Huang et al. (2013)](https://doi.org/10.1371/journal.pone.0064317);
- 2024–2025 county-level kindergarten MMR coverage from the [Texas Department of State Health Services](https://www.dshs.texas.gov/immunizations/data/school/coverage);
- 2025 county-level measles cases from the [JHU Measles Tracking Team](https://github.com/CSSEGISandData/measles_data), licensed CC BY 4.0;
- the eight-group contact matrix from Table S1 of [Porphyre et al. (2012)](https://doi.org/10.1371/journal.pone.0047504).

The Italy and Texas mobility operators use **Meta Colocation Maps**, which cannot be redistributed. The Italy analysis uses province-level ADM2/NUTS 3 data from week 13 of 2023; the Texas analysis uses county-level data from week 9 of 2025. Authorized users can request the maps through [Meta Data for Good](https://dataforgood.facebook.com/dfg/tools/colocation-maps) and place them locally using the filenames documented in [`data/README.md`](data/README.md). The repository deliberately ignores those files.

For Italy, colocation probabilities are converted as (C_{ij}\propto C^{\mathrm{coloc}}_{ij}n_j) and normalized to spectral radius one. Importation weights are computed from modeled airport-to-airport passenger flows. For Texas, county-level MMR coverage adjusts susceptibility before the critical landscape is calculated. No missing empirical values are fabricated.

## Run

```bash
python -m pip install -r requirements.txt
jupyter notebook numerical_method.ipynb
```

After placing the authorized Meta inputs:

```bash
jupyter notebook analysis.ipynb
```

See [`data/README.md`](data/README.md) for exact filenames, columns, provenance, and known limitations.
