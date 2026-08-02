# Seasonal Frozen-Ground Strong-Motion Database

## Overview

This repository provides a record-level strong-motion flatfile with seasonal frozen-ground annotations for Japan. The database integrates earthquake source information, KiK-net station and site metadata, source-to-site distance metrics, significant-duration measures, intensity measures, and seasonal frozen-ground annotations within a unified flatfile structure.

The database is intended to support reproducible analyses of strong-motion records under different ground-freezing conditions. Potential applications include data screening, statistical comparison, regression modelling, ground-motion analysis, and investigations of the associations between seasonal frozen-ground conditions and strong-motion characteristics.

## Database scope

- **Time period:** 2016-01-01 to 2025-01-01
- **Moment-magnitude range:** 4.0 ≤ Mw ≤ 6.5
- **Independent earthquake events:** 1,376
- **Strong-motion records:** 34,654
- **KiK-net stations:** 362
- **Frozen records:** 3,791
- **Non-frozen records:** 30,863
- **Number of database fields:** 56

Each row represents one earthquake–station strong-motion record. The first header row identifies the five field groups, and the second header row provides the exact field names.

## Files

- `Seasonal_Frozen_Ground_Strong_Motion_Database.xlsx`  
  Record-level strong-motion flatfile in Microsoft Excel format. The file retains the two-row header structure and field-group information.

- `Seasonal_Frozen_Ground_Strong_Motion_Database.csv`  
  Record-level strong-motion flatfile in comma-separated-value format. The field order and data content are consistent with the XLSX version.

- `Supplementary_Table_1_Data_Dictionary_v1.0.xlsx`  
  Data dictionary containing the definitions, units, data types, sources or calculation methods, categorical codes, and missing-value conventions for all 56 fields.

- `LICENSE`  
  License terms for the original database compilation, metadata structure, and derived annotations distributed through this repository.

## Database structure

The database is organised into five field groups.

### PART I: Basic earthquake information

This part contains 10 fields describing the event identifier, origin time, epicentral coordinates, focal depth, tectonic type, fault-type classifications, JMA magnitude, and moment magnitude.

### PART II: Station and freeze–thaw metadata

This part contains 16 fields describing the KiK-net station, station location, terrain elevation, freezing index, frozen-ground coefficient, estimated freezing depth, record-level ground-freezing status, freeze–thaw transition count, distance to the matched meteorological station, Vs30, and Japanese Vs30-based site class.

### PART III: Source-to-site distance metrics

This part contains three distance measures:

- Epicentral distance (`Repi`)
- Hypocentral distance (`Rhyp`)
- Rupture distance (`Rrup`)

### PART IV: Significant-duration measures

This part contains D5–75 and D5–95 significant durations for the east–west, north–south, and vertical acceleration components.

### PART V: Intensity measures

This part contains the horizontal geometric-mean peak ground acceleration and 5%-damped pseudo-spectral acceleration values at 20 selected periods from 0.05 s to 5.00 s.

## Seasonal frozen-ground annotations

Each KiK-net station was matched to the nearest Japan Meteorological Agency meteorological station within a maximum distance of 30 km. All 362 KiK-net stations were successfully matched.

The record-level ground-freezing status was determined using the mean of the daily mean air temperatures on the day before the earthquake, the earthquake day, and the following day:

- `freeze_thaw_state = 1`: three-day mean temperature < 0 °C
- `freeze_thaw_state = 0`: three-day mean temperature ≥ 0 °C

A complete three-day temperature window was available for 34,618 records. For the remaining 36 records, the daily mean temperature on the earthquake day was used with the same 0 °C threshold.

The freezing index (`FI`) and freeze–thaw transition count were calculated separately for each complete year from 2016 to 2024 and then averaged across the nine years.

For each year, the freezing index was calculated as the accumulated absolute value of daily mean temperatures below 0 °C.

For the freeze–thaw transition count, each day was classified as either below 0 °C or not below 0 °C. A change between these two temperature states on consecutive days was counted as one transition. This variable represents the annual number of temperature-state transitions and does not necessarily represent the number of complete closed freeze–thaw cycles.

The frozen-ground coefficient (`Ea`) was calculated from station latitude, longitude, and terrain elevation. The estimated freezing depth (`ξ`) was calculated from `FI` and `Ea` and is stored in centimetres.

## Strong-motion processing

The database contains three-component surface acceleration records from KiK-net. All retained records have a sampling frequency of 100 Hz and acceleration values expressed in Gal.

The acceleration time series were processed using the workflow described in the associated Data Descriptor. Processing included mean removal, zero padding, and 0.1–30 Hz acausal band-pass filtering.

The processed records were used to calculate:

- Peak ground acceleration
- 5%-damped pseudo-spectral acceleration
- D5–75 significant duration
- D5–95 significant duration

Horizontal PGA and PSA values were calculated as the geometric mean of the east–west and north–south component values.

The released flatfiles contain derived strong-motion measures and associated metadata. Original KiK-net waveform files are not redistributed through this repository.

## Distance and site parameters

Epicentral distance was calculated from the earthquake epicentre and station coordinates using geodesic calculations on the WGS 84 reference ellipsoid.

Hypocentral distance was calculated from epicentral distance and focal depth.

Rupture distance was calculated directly from publicly available finite-fault models where such models were available. All finite-fault models used in this study were obtained from the NIED Source Inversion Analysis database.

For events without a public finite-fault model, empirical rectangular rupture planes were constructed only for interface, intraslab, and shallow-crustal earthquakes with the required source-mechanism parameters. Records for which rupture distance could not be calculated are assigned `-999`, as specified in the data dictionary.

Vs30 was calculated only for stations whose shear-wave velocity profiles completely covered the upper 30 m. Profiles shallower than 30 m were excluded, and no extrapolation was performed.

## Missing values and categorical codes

The value `-999` is used only for fields and circumstances explicitly specified in the data dictionary.

`Unknown` is a valid categorical value for tectonic type or fault type when a reliable classification cannot be assigned. It is not treated as a general missing-value code.

Users should consult `Supplementary_Table_1_Data_Dictionary_v1.0.xlsx` before filtering, interpreting, or analysing individual fields.

## Data sources

The database was compiled using information obtained or derived from the following public data services and datasets:

- NIED K-NET and KiK-net strong-motion records and KiK-net station information
- JMA Unified Hypocenter Catalog provided through the NIED Hi-net data portal
- NIED F-net moment magnitudes, moment tensors, focal-mechanism solutions, and P- and T-axis parameters
- Japan Meteorological Agency daily mean air-temperature observations
- GEBCO_2025 terrain-elevation data
- Slab2 subduction-zone geometry data
- NIED Source Inversion Analysis finite-fault models, where available

This repository does not redistribute original waveform files, earthquake catalogues, meteorological observations, terrain grids, Slab2 files, or finite-fault model files.

Users should consult and cite the corresponding original data providers, datasets, and services when reusing the database.

## Recommended use and limitations

The record-level ground-freezing status was inferred from daily mean air temperatures recorded at the matched JMA meteorological station. It does not represent a direct observation of soil temperature or subsurface freezing conditions at the KiK-net station.

The freezing index, freeze–thaw transition count, frozen-ground coefficient, and estimated freezing depth are station-scale environmental annotations.

The empirical relationship used to estimate freezing depth was not developed specifically for Japanese stations. The estimated freezing depth should therefore be interpreted as an empirical indicator of the station-scale seasonal freezing background rather than as a measured freezing depth or a site-specific engineering design value.

Users should account for the unequal numbers of frozen and non-frozen records and the non-uniform magnitude–distance coverage when conducting statistical comparisons, regression analyses, or predictive modelling.

Users should also consider earthquake source, propagation-path, and site-condition differences when interpreting statistical differences between frozen and non-frozen records.

## Version and release status

This public repository contains the pre-release version of the Seasonal Frozen-Ground Strong-Motion Database v1.0. The database files, data dictionary, and documentation are undergoing final validation.

The formal v1.0 release will be published through GitHub Releases after final validation. Corrections and future updates will be documented in the release notes and identified using updated version numbers.

## License

The original database compilation, metadata structure, and derived annotations distributed through this repository are licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**, subject to the terms provided in the `LICENSE` file.

This license applies only to the original database compilation, metadata structure, and derived annotations distributed through this repository.

It does not replace, modify, or supersede the terms of use of the third-party source datasets and services listed above.

## Citation

Before publication of the associated Data Descriptor, please cite the database using the repository name, version number, and GitHub repository URL:

**Seasonal Frozen-Ground Strong-Motion Database, version 1.0. GitHub repository: https://github.com/JIENI-gif/seasonal-frozen-ground-strong-motion-database**

After publication of the associated Data Descriptor, users should cite the published article and report the database version used in their study.

Users reusing information derived from third-party source datasets should also cite the corresponding original data providers, datasets, and services listed in this README and in the associated Data Descriptor.
