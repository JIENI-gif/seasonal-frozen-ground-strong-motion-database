# Seasonal Frozen-Ground Strong-Motion Database

## Overview

This repository provides a record-level strong-motion flatfile with seasonal frozen-ground annotations for Japan. Each event–station record links strong-motion measures with earthquake source information, source-to-site distance metrics, KiK-net station and site parameters, and air-temperature-based ground-freezing information.

The database supports comparisons of strong-motion characteristics between records classified as frozen and non-frozen. Source and path parameters can be considered when investigating associations between seasonal ground-freezing conditions and strong-motion characteristics.

## Database scope

- Time period: 2016-01-01 to 2025-01-01
- Moment-magnitude range: 4.0 ≤ Mw ≤ 6.5
- Independent earthquake events: 1,376
- Strong-motion records: 34,654
- KiK-net stations: 362
- Frozen records: 3,791
- Non-frozen records: 30,863
- Number of database fields: 54

Each row of the CSV file represents one earthquake–station strong-motion record. The CSV file has one header row containing the field names. Field definitions, units, codes, and missing-value conventions are provided in the data dictionary.

## Files

- [`Seasonal_Frozen_Ground_Strong_Motion_Database.csv`](./Seasonal_Frozen_Ground_Strong_Motion_Database.csv): Record-level strong-motion flatfile containing 34,654 records and 54 fields.
- [`Supplementary_Table_1_Data_Dictionary_v1.0.xlsx`](./Supplementary_Table_1_Data_Dictionary_v1.0.xlsx): Data dictionary containing field definitions, units, data types, sources or calculation methods, categorical codes, and missing-value conventions.
- [`LICENSE`](./LICENSE): License terms for the original database compilation, metadata structure, and derived annotations distributed through this repository.

## Database structure

The 54 fields are arranged in five groups:

### PART I: Basic earthquake information

Nine fields describe the event identifier, origin time, epicentral coordinates, focal depth, tectonic type, type of faulting determined from the P- and T-axis parameters, JMA magnitude, and moment magnitude.

### PART II: Station and seasonal frozen-ground parameters

Fifteen fields describe the KiK-net station and its location, station elevation, freezing index, freezing coefficient, estimated freezing depth, record-level ground-freezing status, distance to the matched meteorological station, Vs30, and Japanese site class. Vs30 and Japanese site class are distinct fields.

### PART III: Source-to-site distance metrics

Three fields provide epicentral distance (`Repi`), hypocentral distance (`Rhyp`), and rupture distance (`Rrup`).

### PART IV: Significant-duration measures

Six fields provide D5–75 and D5–95 significant durations for the east–west, north–south, and vertical acceleration components.

### PART V: Intensity measures

Twenty-one fields provide horizontal peak ground acceleration and 5%-damped pseudo-spectral acceleration at 20 selected periods from 0.05 to 5.00 s.

## Seasonal frozen-ground annotations

Each KiK-net station was matched to a Japan Meteorological Agency (JMA) meteorological station within a maximum distance of 30 km. All 362 KiK-net stations were matched.

Record-level ground-freezing status was assigned using the mean of the daily mean air temperatures on the day before the earthquake, the earthquake day, and the following day:

- `freeze_thaw_state = 1`: three-day mean air temperature < 0 °C
- `freeze_thaw_state = 0`: three-day mean air temperature ≥ 0 °C

A complete three-day temperature window was available for 34,618 records. For the remaining 36 records, the daily mean air temperature on the earthquake day was used with the same 0 °C threshold.

For each complete calendar year from 2016 to 2024, the annual freezing index (`FI`) was calculated as the sum of the absolute values of daily mean air temperatures below 0 °C. The mean of the nine annual values was assigned to the corresponding KiK-net station.

The freezing coefficient (`Ea`) was calculated from station latitude, longitude, and elevation. Estimated freezing depth (`ξ`) was calculated from `FI` and `Ea` and is stored in centimetres. The associated Data Descriptor and data dictionary provide the calculation details.

## Strong-motion processing

The database contains measures derived from three-component KiK-net surface acceleration records. All retained records have a sampling frequency of 100 Hz, and acceleration is expressed in Gal.

Processing included mean removal, zero padding, and application of the same noncausal 0.1–30 Hz band-pass filter to all records. The processed time histories were used to calculate peak ground acceleration, 5%-damped pseudo-spectral acceleration, and D5–75 and D5–95 significant durations. Horizontal PGA and PSA are the geometric means of the corresponding east–west and north–south component values.

This repository distributes derived strong-motion measures and associated metadata, not the original KiK-net waveform files.

## Distance and site parameters

Epicentral distance was calculated from the earthquake epicentre and station coordinates using geodesic calculations on the WGS 84 reference ellipsoid. Hypocentral distance was calculated from epicentral distance and focal depth.

Rupture distance was calculated using publicly available finite-fault models where available. The finite-fault models used in this study were obtained from the NIED Source Inversion Analysis database. For eligible events without a public finite-fault model, empirical rectangular rupture surfaces were constructed using the available earthquake and focal-mechanism parameters. Records for which rupture distance could not be calculated have the missing-value code specified in the data dictionary.

Vs30 was calculated only where the shear-wave velocity profile extended to at least 30 m below the ground surface; shallower profiles were not extrapolated. The Japanese site class is recorded separately from Vs30. Consult the data dictionary for the definitions and codes of both fields.

## Missing values and categorical codes

The value `-999` is used only for fields and circumstances specified in the data dictionary. `Unknown` is a categorical value for tectonic type or type of faulting when a classification could not be assigned; it is not a general missing-value code.

Users should consult [`Supplementary_Table_1_Data_Dictionary_v1.0.xlsx`](./Supplementary_Table_1_Data_Dictionary_v1.0.xlsx) before filtering or interpreting individual fields.

## Data sources

The database was compiled using information obtained or derived from:

- NIED K-NET and KiK-net strong-motion records and KiK-net station information
- JMA Unified Hypocenter Catalog provided through the NIED Hi-net data portal
- NIED F-net moment magnitudes and focal-mechanism information
- JMA daily mean air-temperature observations
- GEBCO_2025 terrain-elevation data
- Slab2 subduction-zone geometry data
- NIED Source Inversion Analysis finite-fault models, where available

This repository does not redistribute original waveform files, earthquake catalogues, meteorological observations, terrain grids, Slab2 files, or finite-fault model files. Users should consult and cite the relevant original data providers when reusing the database.

## Recommended use and limitations

The record-level ground-freezing status was inferred from air temperatures measured at matched JMA meteorological stations. It is not a direct measurement of soil temperature or subsurface freezing at a KiK-net station.

The freezing index, freezing coefficient, and estimated freezing depth are station-level environmental annotations. Estimated freezing depth is an empirical estimate rather than a measured site-specific freezing depth.

Comparisons of frozen and non-frozen records should account for differences in earthquake source, propagation path, site conditions, and the numbers of records in each group.

## Version status

The files on the `main` branch represent the current database revision. The existing GitHub `v1.0` release is an earlier snapshot and does not represent the current 54-field file structure. A versioned release for the current files will be prepared after final verification.

## License

The original database compilation, metadata structure, and derived annotations distributed through this repository are licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0), subject to the terms in [`LICENSE`](./LICENSE).

This license does not replace or modify the terms of use of the third-party datasets and services listed above.

## Citation

Until a versioned archival record for the current files is available, identify the data using this repository URL and the date accessed:

https://github.com/JIENI-gif/seasonal-frozen-ground-strong-motion-database

The existing `v1.0` release should not be cited as the source of the current 54-field files.
