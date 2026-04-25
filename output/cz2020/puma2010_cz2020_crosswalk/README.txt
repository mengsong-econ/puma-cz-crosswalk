PUMA 2010 to CZ 2020 Crosswalk
===============================

Files in this archive
---------------------
puma2010_cz2020_crosswalk.csv   Crosswalk in CSV format
puma2010_cz2020_crosswalk.dta   Crosswalk in Stata format
README.txt                      This file

Variables
---------
puma2010   Seven-character code. The first two digits are the state FIPS code
           and the last five digits are the PUMA code within a state.
cz2020     2020 commuting zone (USDA Economic Research Service, based on
           the Fowler 2024 methodology with an added contiguity constraint).
afactor    Fraction of a PUMA's population that maps to a given CZ.
           Sums to one within each PUMA. To analyze weighted Census data,
           the person weight from the Census needs to be multiplied with
           "afactor".

Citation
--------
Song, M. (2026). The Future of Work: Remote Opportunities and
Female Labor Force Participation.
