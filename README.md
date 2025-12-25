# environ-investment-disparities

Datasets included are sourced from NSF NCAR Research Data Archive. 
- ECMWF ERA5 (Monthly Mean 0.25 Degree Latitude-Longitude Grid): https://gdex.ucar.edu/datasets/d633001/
- NOAA GPCP (Monthly on a 2.5 degree grid): https://gdex.ucar.edu/datasets/d728006/

## Column definitions

| Column name | Column description |
|----------|----------|
| time  | Month identifier (timestamp at the start of the month). Represents the aggregation period for all monthly precipitation values.  |
| geoid  | County (or county-equivalent) GEOID from the U.S. Census cartographic boundary layer used to define polygons. Stable geographic identifier used to join across datasets.  |

## ERA5-derived polygon metadata (suffix _era5)

| Column name | Column description |
|----------|----------|
| county_name_era5  | County (or county-equivalent) name from the polygon layer used for the ERA5 aggregation. |
| state_abbr_era5 | Two-letter USPS state/territory abbreviation for the polygon used in the ERA5 aggregation. |
| county_state_era5  | Concatenated label "county_name, state_abbr" for readability (not intended as a strict unique key). |
| area_m2_era5 | Polygon area in square meters (m²) as carried through xagg from the county polygon layer. |
| precip_mm_era5 | Area-weighted monthly total precipitation depth over the county polygon in mm/month, computed from ERA5 and aggregated using xagg overlap weights. |
| precip_m3_era5 | Monthly precipitation volume over the county polygon in m³/month, computed as (precip_mm_era5 / 1000) * area_m2_era5. |

## GPCP-derived polygon metadata (suffix _gpcp)

| Column name | Column description |
|----------|----------|
| county_name_gpcp | County (or county-equivalent) name from the polygon layer used for the GPCP aggregation (should match the ERA5 polygon naming if the same boundary file is used). |
| state_abbr_gpcp | Two-letter USPS state/territory abbreviation for the polygon used in the GPCP aggregation. |
| county_state_gpcp | Concatenated label "county_name, state_abbr" for readability (not intended as a strict unique key). |
| area_m2_gpcp | Polygon area in square meters (m²) as carried through xagg from the county polygon layer. |
| precip_mm_gpcp | Area-weighted monthly total precipitation depth over the county polygon in mm/month, computed from GPCP Monthly (mm/day converted to mm/month via days-in-month) and aggregated using xagg overlap weights. |
| precip_m3_gpcp | Monthly precipitation volume over the county polygon in m³/month, computed as (precip_mm_gpcp / 1000) * area_m2_gpcp. |

## Notes

``area_m2_*`` should be identical across ERA5 and GPCP if the same county polygon file is used; duplicate columns are retained for provenance/debugging.

``precip_mm_*`` is the appropriate field for “how much rain fell that month” comparisons; precip_m3_* is useful when comparing total water volume across differently sized counties.
