# Utah Snowpack Map

## Purpose
Create an interactive map showing how Utah snowpack compares with the 1991-2020 median. The app provides both a statewide summary and station-level comparisons for engineers, water managers, and Utah residents.

In current mode, "current" means the latest valid NRCS observation available for the station. In historical mode, the app displays observations for the selected date. The app is informational and does not provide forecasts, reservoir calculations, or flood warnings.

## Inputs
- Date picker defaults to the current date in Utah local time (America/Denver).
- Allowed historical date range is October 1, 1991 through today. Future dates are rejected, and station-specific dates outside the station's valid record or 1991-2020 median coverage are unavailable.
- The map uses live active Utah SNOTEL stations that contain snow water equivalent (WTEQ) data.
- Users select a station by clicking its marker on the map.
- Missing, stale, or quality-failed observations are not interpolated or treated as measurements.

## Calculations
- Use snow water equivalent (SWE) in inches, displayed to 0.1 inch.
- For each station, median SWE is the station's NRCS 1991-2020 median for the exact selected calendar day.
- Percent of median SWE = (Current SWE / Median SWE) x 100.
- Calculate from unrounded SWE and median values, then display station percentages as whole percentages.
- Percentages may exceed 100%.
- Exclude missing, stale, and quality-failed observations. Valid observations require AWDB qcFlag=V and qaFlag=A.
- Exclude stations with median SWE equal to zero because percent of median is undefined.
- Statewide average = arithmetic mean of valid station percentages, with no station weighting.
- Label this result "Average of valid station percentages (unweighted)".
- Display the valid station count and total eligible station count as coverage.

## Outputs
- Map of approximately 140 Utah SNOTEL stations.
- Colored markers showing percent of median SWE.
- Station name, elevation, SWE, and median SWE.
- A graph comparing this water year's SWE to the historical median.
- Statewide average percent of median.

## Look and Feel
- Clean, easy-to-read layout with a large Utah map.
- Summary information at the top.
- Station details and graph appear when a marker is clicked.
- Layout should work on desktop and mobile.

## Validation
Compare SWE and percent of median for three stations against NRCS Utah Snow Survey reports.

Hand calculation example:
- SWE = 12 inches
- Median SWE = 15 inches
- Percent of median = (12 / 15) × 100 = 80%

These are example values and will be replaced with actual NRCS data.

## Out of Scope
- Predicting future snowfall.
- Calculating reservoir storage.
- Providing flood warnings.