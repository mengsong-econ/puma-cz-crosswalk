# PUMA-to-CZ Crosswalks

Crosswalks between Public Use Microdata Areas (PUMAs) and Commuting Zones (CZs)
for use with American Community Survey (ACS) and decennial Census microdata.
Covers PUMA vintages 1990, 2000, 2010, and 2020, mapped to both CZ 1990
(Tolbert and Sizer 1996) and CZ 2020 (Fowler 2024).

## A note to users

This repository provides two versions of crosswalks: **CZ 1990** (the long-standing
Tolbert-Sizer definition, popularized by Autor and Dorn) and **CZ 2020** (the
recent USDA Economic Research Service release based on Fowler 2024).
The crosswalk files are ready for direct use — each CSV or `.dta` file can
be merged onto PUMA-level microdata using the `puma` identifier and weighted
by the `afactor` column.

For full methodological details, see `construction_details.pdf`, which
reproduces the construction appendix of the paper. For context on why these
crosswalks were built and how they are used in empirical work, see
`full_paper.pdf`.

## Contents

### CZ 1990 crosswalks (`output/cz1990/`)

| Folder | PUMA vintage | CZ vintage | Notes |
|---|---|---|---|
| `puma1990_cz1990_crosswalk/` | 1990 | 1990 | Replicates Autor and Dorn (2013) |
| `puma2000_cz1990_crosswalk/` | 2000 | 1990 | Replicates Autor and Dorn (2013) |
| `puma2010_cz1990_crosswalk/` | 2010 | 1990 | Replicates Autor, Dorn, and Hanson (2019) |
| `puma2020_cz1990_crosswalk/` | 2020 | 1990 | New; chained through PUMA 2010 |

### CZ 2020 crosswalks (`output/cz2020/`)

| Folder | PUMA vintage | CZ vintage | Notes |
|---|---|---|---|
| `puma2010_cz2020_crosswalk/` | 2010 | 2020 | New; chained through PUMA 2020 |
| `puma2020_cz2020_crosswalk/` | 2020 | 2020 | New; direct via 2020 counties |

Each crosswalk folder contains:
- A `.csv` file for general use
- A `.dta` file for Stata users
- A `README.txt` with column definitions

### Construction code (`code/`)

- `code/cz1990/puma_cz1990_github.ipynb` — builds all CZ 1990 crosswalks
- `code/cz2020/puma_cz20_github.ipynb` — builds all CZ 2020 crosswalks

### Documentation

- `construction_details.pdf` — detailed methodology appendix
- `full_paper.pdf` — the paper in which these crosswalks are used

## File format

Each crosswalk CSV has three columns:

| Column | Description |
|---|---|
| `puma` | PUMA identifier (state FIPS + PUMA code) |
| `cz` | Commuting zone identifier |
| `afactor` | Population-share allocation factor |

The allocation factor is the share of the PUMA's population residing in the CZ,
measured from the decennial census that defined the PUMA vintage. For each
PUMA, allocation factors sum to one across its CZs. The factor can be
interpreted as the probability that a person drawn at random from the PUMA
lives in that CZ.

## Methodology

Two ideas unify the construction of these crosswalks.

First, each allocation factor is a population share. For a given (PUMA, CZ)
pair, it equals the share of the PUMA's population residing in that CZ,
measured from the decennial census that defined the PUMA vintage. For example,
a PUMA 2020 that splits 70/30 across two CZ 2020s generates two rows in the
crosswalk with factors 0.70 and 0.30.

Second, when the PUMA vintage and the CZ vintage share a common county base,
the crosswalk merges directly through the county. When they do not, the
crosswalk chains through an intermediate PUMA vintage using the IPUMS PUMA
equivalency files. In the chained case, the allocation factor for a
(source PUMA, CZ) pair is the product of the source-PUMA-to-intermediate-PUMA
population share and the intermediate-PUMA-to-CZ population share, summed over
all intermediate PUMAs that the source PUMA overlaps.

For CZ 1990, the PUMA 1990, 2000, and 2010 crosswalks replicate the published
files of Autor and Dorn (2013) and Autor, Dorn, and Hanson (2019). The PUMA
2020 crosswalk extends this coverage by chaining through PUMA 2010 using the
IPUMS PUMA 2010-to-2020 equivalency file. For CZ 2020, which is built on
2020-era county geographies, the PUMA 2020 crosswalk is constructed directly
through 2020 counties, and the PUMA 2010 crosswalk is obtained by chaining
through PUMA 2020.

See `construction_details.pdf` for the full methodology.

## Citation

If you use these crosswalks in your research, please cite the paper:

> Song, Meng. 2026. "The Future of Work: Remote Opportunities and Female
> Labor Force Participation." Working paper.

## References

- Autor, David H., and David Dorn. 2013. "The Growth of Low-Skill Service
  Jobs and the Polarization of the US Labor Market." American Economic
  Review 103(5): 1553–1597.
- Autor, David, David Dorn, and Gordon Hanson. 2019. "When Work Disappears:
  Manufacturing Decline and the Falling Marriage Market Value of Young Men."
  American Economic Review: Insights 1(2): 161–178.
- Fowler, Christopher S. 2024. "New Commuting Zone Delineation for the US
  Based on 2020 Data." Scientific Data 11(1): 975.
- Tolbert, Charles M., and Molly Sizer. 1996. "U.S. Commuting Zones and
  Labor Market Areas: A 1990 Update." Economic Research Service Staff
  Paper 9614.
- U.S. Department of Agriculture, Economic Research Service. 2024.
  Commuting Zones and Labor Market Areas. Washington, DC: USDA Economic
  Research Service. https://www.ers.usda.gov/data-products/commuting-zones-and-labor-market-areas
  (accessed April 2026).

## License

This project is released under the Creative Commons Attribution 4.0
International License (CC BY 4.0). See `LICENSE` for details.

## Contact

Meng Song  
Department of Economics, University of Connecticut  
mengsong.econ@gmail.com