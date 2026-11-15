# HALO dataset - sources (retrieved 13-14 Nov 2026, UTC)

The tables in this folder are the Feature 3 package (see `README.md`), rebuilt from the four files in `raw/` by `prepare_feature3.py`. This page records where those raw files came from.

All data downloaded from NASA data services.

| File | NASA service | Dataset ID | Measured / produced by | Period covered |
|---|---|---|---|---|
| inspiration4_labs_long.csv, inspiration4_labs_wide.csv, inspiration4_baseline_summary.csv (blood count) | NASA Open Science Data Repository | OSD-569, version-4 folder | SpaceX Inspiration4 crew study led by Weill Cornell Medicine | L-92 to R+194 (2021-22) |
| same files (blood chemistry, heart and vessel markers, immune markers) | NASA Open Science Data Repository | OSD-575, version-3 folder | same study | same |
| radiation_5min.csv, radiation_model_train.csv, radiation_model_test.csv | NASA OSDR RadLab | instrument DosTel1, ISS Columbus module | DosTel detector (German Aerospace Center, DLR - not verified against RadLab documentation) | 1 May 2024 00:00 to 30 May 2024 23:55 UTC |
| space_weather_events.csv, storm index | NASA DONKI, GST | 5 storms | Kp values from NOAA (stated in each DONKI record) | 2-17 May 2024 |
| space_weather_events.csv, solar particle events | NASA DONKI, SEP | 14 events | DONKI event catalogue | 9-13 May 2024 |

## Exact addresses
| Data | Address |
|---|---|
| Blood count | nasa-osdr.s3.amazonaws.com/OSD-569/version-4/Complete_Blood_Count/LSDS-7_Complete_Blood_Count_CBC.upload_SUBMITTED.csv |
| Blood chemistry | nasa-osdr.s3.amazonaws.com/OSD-575/version-3/Comprehensive_Metabolic_Panel/LSDS-8_Comprehensive_Metabolic_Panel_CMP.upload_SUBMITTED.csv |
| Heart and vessel markers | nasa-osdr.s3.amazonaws.com/OSD-575/version-3/Multiplex/LSDS-8_Multiplex_serum.cardiovascular.EvePanel_SUBMITTED.csv |
| Immune markers | nasa-osdr.s3.amazonaws.com/OSD-575/version-3/Multiplex/LSDS-8_Multiplex_serum_immune_EvePanel_TRANSFORMED.csv |
| Radiation | visualization.osdr.nasa.gov/radlab/api?instrument_id=DosTel1&timestamp>=2024-05-01&timestamp<2024-05-31&module&absorbed_dose_rate&latitude&longitude&altitude&format=csv (15 two-day slices) |
| Storm index | api.nasa.gov/DONKI/GST?startDate=2024-04-28&endDate=2024-05-31 |
| Solar particle events | api.nasa.gov/DONKI/SEP?startDate=2024-04-28&endDate=2024-05-31 |

## Counts
| Item | Value |
|---|---|
| Radiation readings downloaded | 28,761 |
| Radiation rows (5-minute steps) | 8,627 over 30 days; 13 five-minute bins missing, 6 unbroken segments |
| Space-weather rows | 34 (20 storm-index readings, 14 solar particle events) |
| Blood-test results | 3,190 across 115 tests (20 blood count, 19 blood chemistry, 9 heart and vessel, 67 immune) |
| Astronauts x timepoints | 4 x 7 (L-92, L-44, L-3, R+1, R+45, R+82, R+194) |
| Values set aside for source review | 9 (astronaut C003, L-92 blood count: the rows look shifted in the source table). `value` is blank; the published value and the proposed correction are kept in `labs_source_review.csv`. The earlier pack applied the correction; this one does not. |

## Calculated by us, not downloaded
Every derived column is listed in `data_dictionary.csv`. In short: 5-minute averages, position features, `in_saa_box`, lag and rolling columns, the peak threshold and `target_*` columns, dose totals, `segment_id`, `split`; and for labs the pre-flight baseline, change, z-score, range status and quality flags.

Files were retrieved through a web-fetch tool that converts to text, so they are not byte-identical to NASA's originals.
Blood count and chemistry values were checked against NASA's own processed tables and matched.
