# Analysing-IOD-and-El-Nino-impact-in-Sri-Lanka-s-Rainfall
Term project, B.Sc. (Honours) Data Science and Artificial Intelligence, IIT Guwahati.
Author: **Abilaash Vijeyakumaran**· v.abilaash@op.iitg.ac.in

Continuation of an earlier study of ENSO and monsoon rainfall over India and Sri Lanka
(first adapted from a Madagascar ENSO project, then re-targeted to South Asia).

## Question
Sri Lankan rainfall responds to both El Niño–Southern Oscillation (ENSO) and the Indian Ocean
Dipole (IOD), but the two usually occur together. **Can their effects be separated, and does the
IOD add anything beyond ENSO?** The study also checks links to North Indian Ocean cyclones and
gives a scenario-based outlook for late 2026 and early 2027.

## Main findings (1996–2025, 30 years)
- ENSO and IOD are tightly coupled: SON-mean ONI vs DMI r = 0.70. All seven positive-IOD years
  (by SON mean) were El Niño years.
- Sri Lanka's signal is seasonal: **October** (wetter with El Niño/positive IOD, not separable
  because of collinearity) and **February–April** (drier with El Niño, unchanged after controlling
  for the DMI).
- Cross-validated skill: ONI alone matches or beats ONI+DMI; the DMI adds no out-of-sample skill.
- Cyclone frequency shows no significant ENSO or IOD relationship; only genesis longitude shifts
  with the DMI (exploratory).
- The 2026–27 outlook is scenario-based; all 95% prediction intervals include zero.

## Repository layout
```
notebooks/   IOD_ENSO_SriLanka_Continuation.ipynb   full analysis (Colab/Jupyter)
report/      main.tex, refs.bib, spconf.sty, IEEEbib.bst, figures/, main.pdf
docs/        MISTAKES_AND_FIXES.md                  problems met and how they were fixed
requirements.txt
```

## Data sources (all public; downloaded by the notebook)
| Data | Source |
|---|---|
| ONI | NOAA CPC `oni.ascii.txt` |
| SST for DMI | NOAA OISST v2.1 via CoastWatch ERDDAP |
| Rainfall | CHIRPS v2 (zone means for SW wet and NE dry Sri Lanka) |
| Cyclones | IBTrACS v04r01, North Indian basin |

Raw data are not stored in this repository.

## Method summary
DMI = western (50–70°E, 10°S–10°N) minus south-eastern (90–110°E, 10°S–0°) SST anomaly.
Correlations use effective sample size for autocorrelation, partial correlation to separate ONI
and DMI, and Benjamini–Hochberg control of false discoveries. Seasonal models are scored by
leave-one-year-out skill against climatology. Cyclone counts use Poisson regression with robust
errors. Details and equations are in `report/main.pdf`.

## How to run
1. Open `notebooks/IOD_ENSO_SriLanka_Continuation.ipynb` in Google Colab (or Jupyter).
2. Run cells top to bottom. The OISST download takes a while; ERDDAP sometimes returns 503
   errors, which the notebook retries.
3. The rainfall step expects `precip_zone_checkpoint.csv` from the first study; use the upload
   cell in the notebook.
4. Local setup: `pip install -r requirements.txt`.

## Build the report
Upload `report/` to Overleaf (or run `pdflatex main && bibtex main && pdflatex main && pdflatex main`).

## Limitations
30 years of data, collinear drivers, a 1° sub-sample of OISST, wind-threshold choices for
cyclones, and scenario (not probabilistic) outlooks. Google WeatherNext-type models cover only
about 15 days and cannot be used for 2027.

## Note on AI assistance
AI tools were used during development and drafting, as permitted by the course. The author is
responsible for all analysis choices, results and interpretation.

## License
Code: MIT (add a `LICENSE` file). Data remain under their original providers' terms.
