# Data inputs

Public inputs are included here. The only omitted research data are the restricted Meta Colocation Maps used to reconstruct the Italy and Texas mobility operators.

## Included public data

| File | Contents and source |
|---|---|
| `italy_population.csv` | The 110 GADM-style province identifiers, names, and resident-population values used by the original analysis files. The manuscript does not identify the upstream population release, so the values are preserved rather than silently replaced. |
| `raw/air_travel/AnnualPassengerFlows.csv` | Modeled annual origin–destination passenger flows for the 2010 global air network from Huang et al., *PLOS ONE* 8:e64317, [doi:10.1371/journal.pone.0064317](https://doi.org/10.1371/journal.pone.0064317). Columns: `Destination,Origin,Flow`. |
| `raw/air_travel/AirportInfoWithCountry.csv` | Airport identifiers, names, coordinates, and countries supplied with the Huang et al. flow matrix. |
| `raw/texas_school_coverage_2024_2025.xlsx` | Texas DSHS, “2024–2025 School Vaccination Coverage Levels by District/Private School and County — Kindergarten,” downloaded from the [School Coverage page](https://www.dshs.texas.gov/immunizations/data/school/coverage). |
| `texas_vaccination.csv` | Notebook-ready county MMR coverage extracted from the DSHS workbook. `coverage` is a fraction in `[0,1]`. Loving County is `NR` in the source and is left blank; it is not imputed. |
| `raw/measles_county_all_updates.csv` | Source snapshot downloaded 2026-09-10 from the [JHU Measles Tracking Team repository](https://github.com/CSSEGISandData/measles_data). The source is CC BY 4.0 and is subject to retrospective revision. |
| `texas_measles_cases.csv` | All 254 Texas counties. `cases_2025` is the sum of laboratory-confirmed 2025 county records in the source snapshot; the single record assigned only to `Unknown County` is excluded. `burden_binary` equals one for counties with at least one reported case, matching the paper's burden classification. |
| `la_mrsa_contact_matrix.csv` | Table S1 of Porphyre et al., “A Metapopulation Model to Assess the Capacity of Spread of Meticillin-Resistant *Staphylococcus aureus* ST398 in Humans,” [doi:10.1371/journal.pone.0047504](https://doi.org/10.1371/journal.pone.0047504). Rows are population (i), columns population (j), exactly as published. Two values are reported only as `<0.001` and remain censored rather than being invented. |

LA-MRSA abbreviations are farmers (`F`), farm companion animals (`FCA`), transporters (`T`), slaughterhouse workers (`SHW`), veterinarians (`V`), companion animals (`CA`), general human population (`GH`), and pig veterinarians (`VP`). The paper defines (K_{ij}) as potentially infectious contacts generated in group (i) by an individual in group (j); therefore the source contact table is transposed explicitly when constructing (K).

The Italy importation weights used in the paper are obtained from the two air-travel files. For a source-airport set (\mathcal S) and destination airports (\mathcal D_i) in province (i),

\[
W_i=\frac{\sum_{a\in\mathcal S}\sum_{b\in\mathcal D_i}W_{ab}}
{\sum_j\sum_{a\in\mathcal S}\sum_{b\in\mathcal D_j}W_{ab}}.
\]

The main-text vaccination experiment uses Mexico as the source country. Assigning destination airports to provinces requires a geographic airport-to-province crosswalk; that crosswalk was not present among the inspected source files and has therefore not been fabricated.

## Restricted Meta data

Authorized users can request Colocation Maps through [Meta Data for Good](https://dataforgood.facebook.com/dfg/tools/colocation-maps). Place the authorized extracts here only on your local machine:

- `italy_colocation.csv`: Italy ADM2/NUTS 3, week 13 of 2023. A labeled square CSV with identical row/column province order. Entries are colocation probabilities: the probability that residents of (i) and (j) occupy the same 600 m × 600 m tile in a randomly selected five-minute interval.
- `texas_colocation.csv`: Texas counties, week 9 of 2025, in the same labeled-square format.

These filenames, plus common `colocation`/`facebook` variants and `data/restricted/`, are blocked by `.gitignore` so they cannot be committed accidentally.

## Other analysis inputs

`analysis.ipynb` also documents the expected local `italy_importation.csv`, `texas_population.csv`, and `texas_county_partitions.csv` interfaces. The manuscript identifies the partition sources as the seven Travel Texas regions and the July 2023 U.S. Office of Management and Budget metropolitan-area delineations. Those prepared crosswalks were not present in the inspected source directories, so they are documented but not reconstructed from an unverified substitute.
