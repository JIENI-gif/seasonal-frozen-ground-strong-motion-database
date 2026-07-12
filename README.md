# Seasonal Frozen-Ground Strong-Motion Database

## Overview

This repository provides a record-level strong-motion database with seasonal frozen-ground annotations for Japan. The database integrates earthquake source information, KiK-net station metadata, source-to-site distance metrics, significant-duration measures, intensity measures, and freeze–thaw environmental annotations in a unified flat-file structure.

The database is intended to support reproducible analyses of strong-motion records under different seasonal frozen-ground conditions, including data screening, statistical comparison, regression modelling, and ground-motion studies.

## Database scope

- **Time period:** 2016-01-01 to 2025-01-01
- **Moment-magnitude range:** 4.0 ≤ Mw ≤ 6.5
- **Independent earthquake events:** 1,376
- **Strong-motion records:** 34,654
- **KiK-net stations:** 362
- **Frozen records:** 3,791
- **Non-frozen records:** 30,863
- **Number of database fields:** 56

Each data row represents one earthquake–station strong-motion record. The first header row identifies the five field groups, and the second header row gives the exact field names.

## Files

- `Seasonal_Frozen_Ground_Strong_Motion_Database.xlsx`  
  Record-level database in Microsoft Excel format.

- `Seasonal_Frozen_Ground_Strong_Motion_Database.csv`  
  Record-level database in comma-separated-value format.

- `Supplementary_Table_S1_Data_Dictionary_v1.0.xlsx`  
  Definitions, units, data types, sources or calculation methods, categorical codes, and missing-value conventions for all 56 fields.

- `LICENSE`  
  License terms for the original database compilation, metadata structure, and derived annotations distributed in this repository.

## Database structure

The database is organised into five field groups:

1. **PART I: Basic earthquake information**  
   Event identifier, origin time, epicentral coordinates, focal depth, tectonic type, fault-type classifications, and magnitude information.

2. **PART II: Station and freeze–thaw metadata**  
   KiK-net station information, station coordinates and elevation, freezing index, frost coefficient, estimated frost depth, record-level freeze–thaw state, freeze–thaw cycle count, distance to the matched meteorological station, Vs30, and Japanese Vs30-based site class.

3. **PART III: Source-to-site distance metrics**  
   Epicentral distance, hypocentral distance, and rupture distance.

4. **PART IV: Significant-duration measures**  
   D5–75 and D5–95 significant durations for the east–west, north–south, and vertical components.

5. **PART V: Intensity measures**  
   Horizontal geometric-mean PGA and 5%-damped PSA values at 20 selected periods from 0.05 s to 5.00 s.

## Seasonal frozen-ground annotations

For each strong-motion record, the matched Japan Meteorological Agency meteorological station was identified within 30 km of the KiK-net station.

The record-level freeze–thaw state was determined from the mean of the daily mean temperatures on the day before the earthquake, the earthquake day, and the following day:

- `freeze_thaw_state = 1`: three-day mean temperature < 0 °C
- `freeze_thaw_state = 0`: three-day mean temperature ≥ 0 °C

The freezing index (`FI`) and freeze–thaw cycle count were calculated from the 2016–2025 daily mean temperature series of the matched meteorological station. The frost coefficient (`Ea`) was calculated from station latitude, longitude, and elevation. Estimated frost depth (`ξ`) was calculated from `FI` and `Ea` and is stored in centimetres.

## Strong-motion processing

KiK-net surface three-component acceleration records were processed using the workflow described in the associated Data Descriptor. The released flat files contain derived strong-motion measures and metadata; original waveform files are not redistributed in this repository.

## Missing values

Fields that are unavailable or not applicable use `-999` only where specified in the data dictionary. Users should consult `Supplementary_Table_S1_Data_Dictionary_v1.0.xlsx` before filtering or analysing individual fields.

## Data sources

The database was compiled using information derived from the following public data services:

- NIED KiK-net strong-motion records and station information
- NIED F-net moment magnitudes and focal-mechanism solutions
- NIED Source Inversion Analysis finite-fault models, where available
- Japan Meteorological Agency daily mean temperature observations

This repository does not redistribute original waveform files, original meteorological files, or original finite-fault model files. Users should consult and cite the corresponding source organisations and services when reusing the database.

## Recommended use and limitations

The seasonal frozen-ground fields are environmental annotations rather than direct observations of subsurface thermal or frozen-soil conditions. Estimated frost depth is intended as a station-scale comparative variable and should not be used directly as an engineering design frost depth without site-specific verification.

Users should account for the unequal numbers of frozen and non-frozen records and the non-uniform magnitude–distance coverage when conducting statistical comparisons or predictive modelling.

## Version and release status

This repository is currently being prepared for the public **v1.0** release. After final validation, the repository will be made public, archived through Zenodo, and assigned a DOI. The DOI and formal citation will then be added to this section.

## License

The original database compilation, metadata structure, and derived annotations distributed in this repository are licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**, subject to the terms in the `LICENSE` file.

The license does not replace or modify the terms of the third-party source data services listed above.

## Citation

A formal citation and Zenodo DOI will be added after publication of the v1.0 release.

When using the database before DOI assignment, cite the repository name and version and acknowledge the original data providers.
