# Data inputs

No empirical data are distributed in this repository. In particular, the Meta Colocation Maps used for Italy and Texas are restricted and must not be committed.

Authorized users can request Colocation Maps through [Meta Data for Good](https://dataforgood.facebook.com/dfg/tools/colocation-maps). The paper uses Italy province-level data (ADM2/NUTS 3, week 13 of 2023) and Texas county-level data (week 9 of 2025). Place authorized extracts in this directory only on your local machine.

Expected files:

- `italy_colocation.csv`: square CSV; first column is the province label and remaining column labels match it in the same order. Entries are colocation probabilities.
- `italy_population.csv`: columns `stratum,population`.
- `italy_importation.csv`: columns `stratum,weight`; weights are relative air-travel importation risks.
- `texas_colocation.csv`: square CSV in the same labeled format, at county resolution.
- `texas_population.csv`: columns `stratum,population`.
- `texas_vaccination.csv`: columns `stratum,coverage`, with coverage as a fraction from 0 to 1.
- `texas_measles_cases.csv`: county identifier and observed 2025 measles burden used in the paper.
- `texas_county_partitions.csv`: county identifier plus administrative-region and metropolitan-area labels.
- `la_mrsa_contact_matrix.csv`: the public eight-group contact matrix from the LA-MRSA source cited by the paper, stored as a labeled square CSV without changing its orientation.

Population, vaccination, measles, air-travel, partition, and LA-MRSA inputs should be obtained from the sources cited in the paper and checked against their licenses. They are not fabricated or silently substituted here.

The repository `.gitignore` excludes everything in `data/` except this README. If a small public input is later added, review its license and add an explicit allow-list rule before committing it.
