# Utah Snowpack Map

## App Overview
The Utah Snowpack Map is an informational app for viewing Utah's active SNOTEL stations against the NRCS 1991-2020 median. It presents an unweighted statewide average and valid-station coverage, an interactive color-coded map, station measurements and water-year SWE graphs, and clear data-quality or unavailable states. After required functionality passes validation, the app adds station comparison and a station data-quality panel. Forecasts, alerts, reservoir calculations, and data exports are out of scope.

## Purpose
Create an interactive map showing how Utah snowpack compares with the 1991-2020 median. The app provides both a statewide summary and station-level comparisons for engineers, water managers, and Utah residents.

Selecting today's date in America/Denver uses current mode: retrieve recent hourly NRCS WTEQ observations and show the latest actual measurement with its timestamp, even when its QA flag is Raw (`R`) or Provisional (`P`). Identify readings whose QA flag is not Approved (`A`) as unapproved, show their SWE separately, and do not calculate percent of median or include them in the statewide average. Use the station's AWDB `dataTimeZone` offset and the hourly observation timestamp to enforce the 24-hour freshness limit. Only current observations passing the approved quality checks and nonzero-median rule may be used for percent-of-median markers and statewide calculations.

Selecting an earlier date uses historical mode: use only a DAILY observation from that exact selected date, and apply the existing `qcFlag=V` and `qaFlag=A` requirements. Do not substitute or interpolate SWE observations. The app is informational and does not provide forecasts, reservoir calculations, or flood warnings.

## Inputs
- Date picker defaults to the current date in Utah local time (America/Denver).
- Allowed historical date range is October 1, 1991 through today. Future dates are rejected, and station-specific dates outside the station's valid record or 1991-2020 median coverage are unavailable.
- The map uses live active Utah SNOTEL stations that contain snow water equivalent (WTEQ) data.
- Current mode uses recent HOURLY WTEQ data; historical mode uses DAILY WTEQ data for the exact selected date.
- Users select a station by clicking its marker on the map.
- The eligible-station denominator includes every active Utah SNOTEL station with SWE monitoring capability, even when its observation or median SWE is unavailable for the selected date.
- The valid-station numerator includes only stations with an acceptable observation for the selected mode and date, valid AWDB quality flags, a current-mode observation age of no more than 24 hours when applicable, and a nonzero median SWE.
- Missing, stale, or quality-failed observations are not interpolated or treated as measurements.
- Current mode may display a real hourly SWE value flagged Raw (`qaFlag=R`) or Provisional (`qaFlag=P`) as unapproved, with its AWDB timestamp and station time-zone offset. These readings are excluded from percent-of-median markers and the statewide average.

## Calculations
- Use snow water equivalent (SWE) in inches, displayed to 0.1 inch.
- For each station, median SWE is the station's NRCS 1991-2020 median for the exact selected calendar day.
- Current-mode hourly SWE has no hourly median in the AWDB response. Retrieve the official daily median using an AWDB DAILY request for the same month and day in a year with an available daily record. Use only that response's `median` field, which represents the 1991-2020 median; never use its SWE `value` as a substitute for the current hourly SWE.
- Percent of median SWE = (Current SWE / Median SWE) x 100.
- Calculate from unrounded SWE and median values, then display station percentages as whole percentages.
- Percentages may exceed 100%.
- Exclude missing, stale, and quality-failed observations. Valid observations require AWDB qcFlag=V and qaFlag=A.
- AWDB QA flags used in current mode: `R` = Raw, `P` = Provisional, and `A` = Approved. Raw and Provisional SWE may be displayed with explicit status but are not valid for percentages or statewide calculations.
- In current mode, calculate observation age from the hourly timestamp interpreted with the station's AWDB `dataTimeZone` offset. Observations older than 24 hours are stale and excluded from calculations.
- Exclude stations with median SWE equal to zero because percent of median is undefined.
- Statewide average = arithmetic mean of valid station percentages, with no station weighting.
- Label this result "Average of valid station percentages (unweighted)".
- Display the valid station count divided by the total eligible station count as coverage. The denominator includes all active Utah SNOTEL stations with SWE monitoring capability; the numerator includes only stations passing the approved observation, quality, date, and nonzero-median rules.

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
- In current mode, display the latest available hourly SWE and timestamp even for Raw or Provisional readings. Label unapproved or stale readings clearly, display percent of median as unavailable when quality/date/freshness rules fail, and exclude them from statewide calculations.
- For the current-mode median lookup, identify that the daily `median` field is sourced from the same calendar day; do not imply that the lookup year's SWE value is the current observation.
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
- In current mode, show the most recent hourly SWE timestamp with the AWDB station time-zone offset and observation age; use text labels for Raw, Provisional, Approved, stale, and unavailable statuses.
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
- Future snowfall and water-supply forecasting.
- Reservoir storage calculations.
- Flood warnings and emergency alerts.
- Snow-course and other non-SNOTEL measurements.
- Basin, county, and water-supply forecasts.
- Irrigation demand and agricultural recommendations.
- Historical data downloads or exports.

Historical date selection and historical SWE visualization remain included in the app.

The app is informational only and is not a replacement for official NRCS reports or professional engineering judgment.

## Features

The following features are additional capabilities and are distinct from the required app functionality. They must be implemented only after all required app functionality passes validation.

### Feature 1: Station Comparison Mode

- Users activate station comparison mode with a toggle.
- Comparison mode allows selecting up to three Utah SNOTEL stations.
- A compact comparison table displays each selected station's SWE, median SWE, percent of median, and data availability.
- Use the existing SWE, median SWE, and percent-of-median calculations; no additional snowpack formula is needed.
- Overlay the selected stations' water-year SWE measurements on a shared responsive graph.
- Prevent selecting more than three stations and provide controls for removing selected stations.
- Keep unavailable selected stations in the comparison table and omit their unavailable graph series.
- Missing, invalid, stale, zero-median, and exact-date-unmatched measurements remain unavailable under the existing rules.
- Comparison mode uses the currently selected date and AWDB triplet/observation data.

### Feature 2: Station Data-Quality Indicator

- Add an expandable data-quality section within the existing station details panel.
- Show the observation date, observation timestamp, observation age, AWDB qcFlag, AWDB qaFlag, median availability, NRCS/AWDB source, station identifier/triplet, and effective data status.
- Explain in plain text why a measurement is unavailable or excluded, including missing data, invalid quality flags, a stale observation, median SWE equal to zero, or failure to match the exact historical date.
- In current mode, apply the existing 24-hour stale-data rule.
- In historical mode, require exact selected-date matching and do not substitute or interpolate observations.
- This feature uses existing AWDB metadata and data values and does not introduce a separate calculation or external data source.

## Build stages

Build and review one stage at a time. Do not begin a later stage until the preceding stage is complete and approved. Station Comparison Mode and the Station Data-Quality Indicator must not be built until all required functionality has passed Stage 4 validation.

### Stage 1: Initial page mockup

**What will be built:**
- A single-page layout with the statewide summary and date picker at the top, a Utah map area on the left, and a station detail and graph area on the right.
- Responsive desktop and mobile layouts using placeholder content only.

**What to test or check:**
- Check layout hierarchy, readability, responsive stacking, legend placement, and visible keyboard focus.
- Confirm no live NRCS data or calculations are presented as real in the mockup.

**Completion criteria:**
- The approved page structure is clear and readable at desktop and mobile widths, and all displayed data is visibly identified as placeholder content.

### Stage 2: Interactive Utah SNOTEL map

**What will be built:**
- A Utah map populated with mock station data, including zoom and pan, marker colors and legend, tooltips/tap interactions, and station selection by pointer or keyboard.

**What to test or check:**
- Check marker selection, marker overlap and zooming, accessible station selection, marker color bins, and solid-gray unavailable markers with text status.

**Completion criteria:**
- Users can inspect and select mock stations at desktop and mobile sizes, and the map interactions and legend follow the approved specification.

### Stage 3: NRCS API, calculations, station details, and graphs

**What will be built:**
- NRCS AWDB station metadata and observation integration.
- Current mode uses recent hourly WTEQ observations and station `dataTimeZone` offsets for the 24-hour age check; historical mode uses exact-date daily WTEQ observations.
- Current-mode daily median lookup uses only the official AWDB `median` field for the same calendar day and never reuses a prior year's actual SWE value.
- Current/historical mode behavior, SWE and median calculations, statewide summary and coverage, station details, and selected water-year SWE and 1991-2020 median graphs.
- Loading, unavailable, API failure, last-known-data, and retry states.

**What to test or check:**
- Check today's America/Denver date uses current mode and the 24-hour stale threshold; earlier dates use exact-date historical mode.
- Check current Raw (`R`) and Provisional (`P`) hourly SWE is displayed with its timestamp and unapproved status but remains unavailable for percent-of-median markers and the statewide average.
- Check AWDB quality flags, missing values, zero medians, units, rounding, map classification, statewide numerator and denominator, graph labels, and missing-data gaps.

**Completion criteria:**
- Live AWDB-backed values appear with correct station/date context; invalid or unavailable data is excluded and communicated under the specified rules; station detail and graph values agree.

### Stage 4: Required-functionality validation

**What will be built:**
- Focused validation tests and recorded results for the required app functionality. No additional product feature is added in this stage.

**What to test or check:**
- Check the Brighton hand calculation and all three April 1, 2025 AWDB station references within the stated SWE and percentage criteria.
- Exercise missing observations, invalid quality flags, zero median SWE, stale current observations, and historical exact-date matching.
- Compare station values only; do not compare the app's unweighted statewide average to an NRCS basin-weighted statistic.

**Completion criteria:**
- Required validation cases pass and results are documented before optional features begin.
- Independent comparisons against downloadable NRCS Utah Snow Survey reports remain explicitly pending until those reports are obtained and compared; do not claim those comparisons passed before then.

### Stage 5: Station Comparison Mode

**What will be built:**
- The comparison toggle, selection/removal controls for up to three stations, comparison table, and shared water-year SWE graph.

**What to test or check:**
- Check the three-station limit, removal, metric consistency with the required station details, and unavailable stations remaining in the table while their graph series are omitted.

**Completion criteria:**
- One to three stations can be compared using the existing validated calculations, without changing required map or station behavior.

### Stage 6: Station Data-Quality Indicator

**What will be built:**
- The expandable data-quality section in station details, including observation date, timestamp, age, AWDB flags, median availability, source, station identifier, effective status, and explanation.

**What to test or check:**
- Check displayed diagnostic values and explanations for valid, missing, invalid-quality, stale, zero-median, and historical exact-date-unmatched cases.
- Confirm the 24-hour rule applies only to current mode.

**Completion criteria:**
- The panel accurately describes the data used or the reason it is excluded, following the validated current/historical rules.