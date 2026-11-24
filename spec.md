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
- A Utah map of live active Utah SNOTEL stations that contain WTEQ data.
- A five-level, visible marker color scale based on percent of median SWE:
  - 0-49%
  - 50-79%
  - 80-119%
  - 120-149%
  - 150% or higher
- Use unrounded station percentages for marker classification and only round whole percentages for display.
- Display missing, invalid, stale, or zero-median stations as solid gray markers.
- Exclude gray markers from the statewide average and explain the station's unavailable status in the tooltip or station details.
- A station detail panel containing station name, elevation, selected date, observation timestamp, SWE, median SWE, percent of median, and NRCS source information.
- SWE and median SWE are in inches and displayed to 0.1 inch; percent of median is displayed as a whole percentage.
- A two-line station SWE graph spanning October 1 through the selected date:
  - selected water year's SWE
  - 1991-2020 median SWE
- Label the graph axes as SWE (inches) and Date, and display missing observations as gaps rather than interpolated values.
- A statewide summary labeled "Average of valid station percentages (unweighted)" with the valid/eligible station count.
- A visible legend explaining the marker color scale and solid-gray unavailable state.
- A sortable station table and CSV downloads are out of the initial build.

## Look and Feel
- Use a clean, professional, engineering-focused layout with clear hierarchy and readable text.
- On initial load, display the statewide snowpack summary, date picker, and full Utah SNOTEL map.
- Do not automatically show a selected station's details or three-station validation summary.
- On desktop, place the large interactive Utah map on the left and station details plus the SWE graph on the right.
- On mobile, stack the statewide summary, date picker, map, station details, and graph vertically.
- Allow users to zoom and pan the map so overlapping SNOTEL markers can be distinguished.
- Show hover tooltips on desktop and tap interactions on mobile.
- Clicking or keyboard-selecting a station opens its details and SWE graph.
- Provide clear loading states while station metadata or observations are loading.
- Display clear unavailable-data messages for missing, invalid, stale, or out-of-range observations.
- If an NRCS API request fails, preserve previously loaded data, label it explicitly as last-known data, and show a Retry button.
- Treat a current-mode observation as stale and unavailable after 24 hours.
- Historical observations must match the exact selected date; do not show an earlier or interpolated observation.
- Make SWE graphs responsive and preserve readable axis labels and units on narrow screens.
- Show gaps rather than connecting across missing historical observations.
- Display a visible map legend for all five marker color ranges and the solid-gray unavailable state.
- Use sufficient color contrast and accessible text labels.
- Station selection and Retry controls must support keyboard focus and visible focus indicators.
- Status, unavailable, stale, and last-known-data indicators must not rely on color alone.
- Default the date picker to today's date in America/Denver and prevent future dates.

## Validation
Initial station-level reference values are obtained from the NRCS AWDB for April 1, 2025:

| Station | Triplet | SWE | 1991-2020 median SWE | Percent of median |
|---|---|---:|---:|---:|
| Brighton | 366:UT:SNTL | 21.4 inches | 21.6 inches | 99% |
| Snowbird | 766:UT:SNTL | 38.6 inches | 36.5 inches | 106% |
| Ben Lomond Peak | 332:UT:SNTL | 33.4 inches | 33.4 inches | 100% |

Brighton hand calculation:
- SWE = 21.4 inches
- Median SWE = 21.6 inches
- Percent of median = (21.4 / 21.6) x 100 = 99.074%, displayed as 99%

The official AWDB source is:
- Base data endpoint: `https://wcc.sc.egov.usda.gov/awdbRestApi/services/v1/data`
- API documentation: `https://wcc.sc.egov.usda.gov/awdbRestApi/v3/api-docs`
- Station metadata endpoint: `https://wcc.sc.egov.usda.gov/awdbRestApi/services/v1/stations`

The validation query uses station triplets `366:UT:SNTL,766:UT:SNTL,332:UT:SNTL`, element `WTEQ`, duration `DAILY`, begin and end date `2025-04-01`, `centralTendencyType=MEDIAN`, `returnFlags=true`, and `periodRef=END`.

Calculate with unrounded values and round only SWE and percentage output as specified by the Calculations and Outputs sections.

Acceptance criteria:
- SWE matches the AWDB reference within 0.1 inch.
- Percent of median matches the displayed nearest whole-percent result.
- Brighton, Snowbird, and Ben Lomond Peak must each pass independently.
- The app's unweighted station average must not be compared directly with an NRCS basin-weighted statewide statistic.

Historical-date validation:
- An observation must correspond to the exact selected date.
- Do not substitute an earlier observation, later observation, or interpolated value.
- For a missing exact-date observation, display the station as unavailable and exclude it from the statewide average.

Edge-case tests:
- Missing observation: show unavailable and exclude it from marker classification and the statewide average.
- Invalid quality flags: require `qcFlag=V` and `qaFlag=A`; otherwise show unavailable and exclude it.
- Zero median SWE: show unavailable and exclude it because percent of median is undefined.
- Stale observation: show unavailable and exclude it; a stale test fixture must fail the applicable observation-age or station-report-time rule rather than be converted to valid SWE.

Independent comparison against downloadable NRCS Utah Snow Survey reports is still pending. The app is not yet implemented, and validation has not passed.

## Out of Scope
- Predicting future snowfall.
- Calculating reservoir storage.
- Providing flood warnings.