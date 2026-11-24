# Utah Snowpack Map

## Purpose
Create an interactive map showing how Utah's current snowpack compares to normal. The app is intended for engineers, water managers, and Utah residents.

## Inputs
- Date picker (defaults to today).
- Users can select a SNOTEL station by clicking its marker on the map.

## Calculations
- Percent of median SWE = (Current SWE / Median SWE) × 100.
- Statewide average = average of valid station percentages.

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