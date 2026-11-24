# AI Prompt Log

## Prompt 1 - Initial Specification Review

**Prompt:**
I am building a Utah Snowpack Map web app for an engineering
assignment. Read spec.md and review all seven sections.

Do not write or modify any code or files yet.

Identify important missing requirements, unclear assumptions,
and potential problems with the NRCS API, historical SWE data,
and percent-of-median calculations.

Ask me five specific questions that would help improve the
specification. Explain why each question matters.

**Agent Response / Decisions:**
- Identified NRCS AWDB REST API as the data source.
- Proposed using the 1991-2020 median.
- Recommended an unweighted statewide average.
- Proposed plotting SWE from October 1 through the selected date.
- Recommended validating three stations against NRCS reports.
- Identified missing, stale, quality-failed, and zero-median
  observations as important considerations.

**Result:**
Planning review completed. No files were modified.
Further validation decisions are needed.

## Prompt 2 - Validation and Median Decisions

**Prompt:**
Please decide the remaining validation and calculation details:
the median period and date basis, statewide aggregation and missing-value
rules, graph date window and series, and the three-station validation set,
precision, and acceptance criteria.

**Agent Response / Decisions:**
- Selected the NRCS AWDB REST API.
- Chose the 1991-2020 median reference period.
- Defined the statewide result as an unweighted average of valid station
  percent-of-median values.
- Planned to exclude missing, stale, quality-failed, and zero-median stations.
- Chose October 1 through the selected date for the current water-year graph.
- Proposed reporting SWE to 0.1 inch and percent of median to the nearest whole
  percent.

**Result:**
Planning decisions were recorded by the assistant. No files were modified.

## Prompt 3 - Refine Validation Section

**Prompt:**
Use Brighton (366), Snowbird (766), and Ben Lomond Peak (332) for validation.
Use April 1, 2025 as a historical validation date and November 23, 2026 as an
additional fall test. Keep the 1991-2020 median period. Identify where to obtain
matching NRCS station-level SWE and median values. Explain handling for zero
median SWE, missing observations, and historical dates. Do not invent
measurements. Ask for any remaining decisions needed to complete Validation
and Calculations.

**Agent Response / Decisions:**
- Identified the NRCS AWDB REST API and Report Generator as authoritative sources.
- Verified station triplets: Brighton 366:UT:SNTL, Snowbird 766:UT:SNTL, and
  Ben Lomond Peak 332:UT:SNTL.
- Retrieved April 1, 2025 AWDB station-level values: Brighton 21.4 inches SWE
  and 21.6-inch median; Snowbird 38.6 inches SWE and 36.5-inch median;
  Ben Lomond Peak 33.4 inches SWE and 33.4-inch median.
- Calculated the corresponding percentages as 99%, 106%, and 100%.
- Determined that the November 23, 2026 AWDB query returned no observations,
  so no fall measurements were invented.
- Confirmed date bounds, missing-value behavior, quality flags, zero-median
  behavior, and station-specific historical coverage.

**Result:**
Planning review completed. No files were modified.

## Prompt 4 - Maintain Prompt Log

**Prompt:**
Please read AGENTS.md and begin automatically maintaining prompts.md. After
every request, record my prompt, a summary of my response, all decisions made,
and every file changed. Include previous planning interactions from this
conversation. Do not overwrite existing entries. Continue throughout the project.

**Agent Response / Decisions:**
- Read AGENTS.md and confirmed its prompt-log requirement.
- Reviewed prompts.md and identified the existing first-entry-only log.
- Appended entries for the previous planning interactions and this maintenance
  request.
- Made no specification or implementation changes.

**Files Changed:**
- `prompts.md`: appended Prompt 2, Prompt 3, and this Prompt 4 entry.

**Result:**
Automatic prompt logging instructions were implemented for the conversation.

## Prompt 5 - Review Purpose, Inputs, and Calculations

**Prompt:**
Continue improving spec.md. Based on the previous discussion, review the
Purpose, Inputs, and Calculations sections one at a time. For each section:
1. Identify missing requirements.
2. Recommend reasonable defaults, ranges, and units.
3. Explain potential problems or edge cases.
4. Ask questions before making changes.
Do not modify spec.md or build the app. Update prompts.md to record the
conversation.

**Agent Response / Decisions:**
- Read the current Purpose, Inputs, and Calculations sections.
- Prepared a section-by-section review and a set of decisions needed before
  specification changes.
- No specification or implementation decisions were finalized.

**Files Changed:**
- `prompts.md`: appended this Prompt 5 entry.

**Result:**
Planning review in progress. `spec.md` was not modified and the app was not built.

## Prompt 6 - Update Purpose, Inputs, and Calculations

**Prompt:**
Approve using Utah local time (America/Denver) for the default date.
Approve labeling the statewide summary "Average of valid station percentages
(unweighted)." Keep excluding invalid observations and zero-median stations,
not interpolating missing data, and allowing percentages above 100%.
Update the Purpose, Inputs, and Calculations sections of spec.md only. Continue
logging; do not build the app. Then identify the next four sections to review.

**Agent Response / Decisions:**
- Updated the Purpose section to distinguish statewide and station-level
  comparisons, define current versus historical mode, and establish the
  1991-2020 median period.
- Updated Inputs to use America/Denver for the default date, limit historical
  dates to October 1, 1991 through today, use live active Utah SNOTEL stations
  with WTEQ, and prohibit interpolation.
- Updated Calculations to specify exact-calendar-day medians, inches and
  display precision, whole-percent station output, percentages above 100%,
  quality and missing-value exclusions, zero-median exclusion, unweighted
  statewide averaging, and valid/eligible station coverage.
- Recommended reviewing Outputs next, followed by Validation, Look and Feel,
  and Out of Scope.

**Files Changed:**
- `spec.md`: updated Purpose, Inputs, and Calculations sections.
- `prompts.md`: appended this Prompt 6 entry.

**Result:**
The approved specification changes were applied. No app code or build artifacts
were created.

## Prompt 7 - Review Outputs Section

**Prompt:**
Review the Outputs section of spec.md. Recommend a clear marker color scale,
missing-data and zero-median marker behavior, graph labels and units, statewide
average and valid station count display, and additional engineering outputs.
Explain recommendations and ask questions about choices. Do not modify spec.md
or build code; only update prompts.md.

**Agent Response / Decisions:**
- Recommended a five-level accessible percent-of-median marker scale:
  0-49%, 50-79%, 80-119%, 120-149%, and 150% or higher.
- Approved choice: unavailable stations use a neutral solid-gray marker rather
  than a dashed-ring marker.
- Missing observations, invalid quality flags, and zero-median stations will
  have explicit unavailable reasons when a station is inspected.
- Recommended the SWE graph use two lines: current water-year SWE and the
  1991-2020 median, in inches, from October 1 through the selected date.
- Missing graph observations should appear as breaks rather than interpolated
  line segments.
- Recommended the top summary show the whole-percent unweighted average and
  valid/eligible station coverage.
- Approved additional outputs: selected-date and station-as-of timestamps,
  NRCS AWDB source link, visible units and legend, and a sortable station table.
- Recommendations should not be added to spec.md until the user approves each
  Output decision during the specification-edit stage.

**Files Changed:**
- `prompts.md`: appended this Prompt 7 entry.

**Result:**
Planning review completed for Outputs. No files other than prompts.md were
modified, and no app code was built.

## Prompt 8 - Apply Approved Outputs Decisions

**Prompt:**
Approve the five-level marker color scale with legend, solid-gray unavailable
markers, the two-line SWE graph from October 1 through the selected date,
statewide unweighted average with valid/eligible station count, and required
station detail fields. Use unrounded values for calculations and classification,
round only for display. Postpone the sortable table and leave CSV downloads out
of the initial build. Update only Outputs in spec.md and continue prompt logging.
Do not build app code.

**Agent Response / Decisions:**
- Updated only the Outputs section of spec.md.
- Added the five marker ranges, visible legend, solid-gray unavailable state,
  missing-data exclusions, and station details.
- Defined SWE and median SWE in inches to 0.1 inch and percent of median as a
  whole percentage.
- Added the two-line October 1-to-selected-date graph, axis labels, median
  reference, and missing-data gaps.
- Added the statewide unweighted average label and valid/eligible station count.
- Explicitly postponed the sortable station table and CSV downloads.

**Files Changed:**
- `spec.md`: updated only the Outputs section.
- `prompts.md`: appended this Prompt 8 entry.

**Result:**
All approved Outputs decisions were applied. No app code or build artifacts
were created.

## Prompt 9 - Prepare Final Validation Section

**Prompt:**
Finalize the planned Validation section for three stations: Brighton (366),
Snowbird (766), and Ben Lomond Peak (332), using April 1, 2025. Find actual NRCS
SWE and 1991-2020 median values, identify official report and API sources,
explain a hand calculation, recommend tolerances and edge-case tests, explain
station-to-report comparison, and do not invent measurements or claim app tests
have passed before implementation. Update prompts.md only.

**Agent Response / Decisions:**
- Verified official AWDB WTEQ observations and medians for April 1, 2025:
  Brighton 21.4/21.6 inches, Snowbird 38.6/36.5 inches, and Ben Lomond Peak
  33.4/33.4 inches.
- Calculated hand percentages as Brighton 99.1%, Snowbird 105.8%, and Ben Lomond
  Peak 100.0%, or 99%, 106%, and 100% to whole-percent display.
- Confirmed source station triplets and valid quality flags for all three
  observations: `qcFlag=V` and `qaFlag=A`.
- Identified the official AWDB metadata and data endpoints plus the NRCS
  Report Generator interface as sources.
- Recommended SWE pass/fail within 0.1 inch and percentage pass/fail within
  nearest whole percent.
- Recommended edge tests for missing values, invalid quality flags, stale
  observations, and median SWE equal to zero.
- Explained that validation should compare station values only and must not
  compare the app's unweighted station average with an NRCS basin-weighted
  statewide statistic.
- Recorded that no app validation test can pass until the app exists.

**Files Changed:**
- `prompts.md`: appended this Prompt 9 entry.

**Result:**
Validation measurements and sources were prepared for specification review.
No `spec.md` changes or app implementation were performed.

## Prompt 10 - Update Validation Section

**Prompt:**
Approve the three April 1, 2025 AWDB station measurements and Brighton as the
hand-calculation example. Require exact selected-date observations with no
fallback or interpolation. Update Validation in spec.md with station values and
percentages, the Brighton calculation, exact AWDB sources/query parameters,
acceptance criteria, and edge-case tests. Clearly state that independent NRCS
Snow Survey report comparisons remain pending and that the app has not passed
validation. Update prompts.md only; do not build app code.

**Agent Response / Decisions:**
- Updated only the Validation section of spec.md.
- Recorded Brighton, Snowbird, and Ben Lomond Peak April 1, 2025 AWDB values
  and nearest-whole-percent results.
- Added Brighton's hand calculation at full precision and display rounding.
- Added the AWDB data, metadata, and API documentation sources plus all validation
  query parameters.
- Added SWE and percentage acceptance tolerances.
- Added exact-date, missing, invalid-quality, zero-median, and stale-observation
  requirements.
- Explicitly stated that independent NRCS report comparison remains pending and
  that the app has not passed validation.

**Files Changed:**
- `spec.md`: updated only the Validation section.
- `prompts.md`: appended this Prompt 10 entry.

**Result:**
The approved Validation section was added. No app code or build artifacts were
created.

## Prompt 11 - Review Look and Feel Preferences

**Prompt:**
Finalize the planned Look and Feel section. Review a clean engineering design
with a left Utah map and right station details on desktop, vertical stacking on
mobile, loading/unavailable/API failure states, the approved marker scale,
mouse and keyboard station selection, responsive graphs, Utah date defaults,
future-date prevention, and accessibility. Identify conflicts or technical
limitations and ask up to three design questions before editing spec.md.
Update prompts.md only; do not build app code.

**Agent Response / Decisions:**
- Reviewed the proposed desktop and mobile layouts against existing outputs,
  calculations, and validation rules.
- Identified remaining design questions for loading/failure behavior, default
  station-detail behavior, and stale-data handling.
- No Look and Feel specification edits or app implementation were performed.

**Files Changed:**
- `prompts.md`: appended this Prompt 11 entry.

**Result:**
Planning review in progress. Look and Feel decisions await clarification.

## Prompt 12 - Finalize Look and Feel Decisions

**Prompt:**
Review the Look and Feel preferences and identify design conflicts, technical
limitations, or missing requirements. Ask up to three questions needed to
finalize design. Do not modify spec.md or build app code; update prompts.md.

**Agent Response / Decisions:**
- Selected API failure behavior: keep the last successful data on screen,
  clearly label it as stale or last-known, and provide a Retry action.
- Selected initial desktop/mobile detail state: show the three-station validation
  summary for Brighton, Snowbird, and Ben Lomond Peak before an individual
  station is selected.
- Selected stale threshold: observations are unavailable after 24 hours in
  current mode. Historical mode remains exact selected-date data and is not
  made unavailable merely because it is old.
- Identified technical considerations: 140 markers need sufficient spacing,
  keyboard access, hover-versus-tap handling, responsive chart labels, API
  partial failures, and non-color-only station status.
- No Look and Feel section edits or app implementation were performed.

**Files Changed:**
- `prompts.md`: appended this Prompt 12 entry.

**Result:**
The remaining Look and Feel decisions were resolved and are ready for a later
specification-edit step.

## Prompt 13 - Update Look and Feel Section

**Prompt:**
Approve the Look and Feel recommendations with one adjustment: open with the
statewide snowpack summary and full Utah SNOTEL map, not a validation summary.
Station details appear after selection. Add desktop and mobile layouts, map
zooming, hover/tap behavior, keyboard selection, loading/unavailable states,
last-known-data API failure behavior with Retry, the 24-hour current-mode stale
threshold, exact historical-date matching, responsive and accessible charts,
visible legend, and sufficient contrast. Update only Look and Feel in spec.md,
maintain prompts.md, do not build app code, and identify remaining Out of Scope
decisions afterward.

**Agent Response / Decisions:**
- Updated only the Look and Feel section of spec.md.
- Added initial statewide summary/map behavior and post-selection station details.
- Added desktop and mobile layout requirements, map zoom, interaction methods,
  loading and unavailable states, API retry behavior, stale-data handling,
  exact-date matching, chart responsiveness, legend, keyboard access, and
  accessible status indicators.
- Identified that Out of Scope still needs only an explicit boundary-review
  confirmation unless additional exclusions are requested.

**Files Changed:**
- `spec.md`: updated only the Look and Feel section.
- `prompts.md`: appended this Prompt 13 entry.

**Result:**
The approved Look and Feel section was applied. No app code or build artifacts
were created.

## Prompt 14 - Update Out of Scope Section

**Prompt:**
Approve all five additional Out of Scope exclusions. Explicitly exclude future
snowfall and water-supply forecasting, reservoir storage, flood warnings and
emergency alerts, non-SNOTEL measurements, basin/county/water-supply forecasts,
irrigation/agricultural recommendations, and historical data downloads/exports.
Clarify that historical date selection and SWE visualization remain included,
and that the app is informational rather than a replacement for NRCS reports or
professional engineering judgment. Update prompts.md and do not build app code.

**Agent Response / Decisions:**
- Updated only the Out of Scope section of spec.md.
- Added all approved exclusions.
- Explicitly preserved historical date selection and historical SWE visualization.
- Added the informational-use and professional-judgment disclaimer.

**Files Changed:**
- `spec.md`: updated only the Out of Scope section.
- `prompts.md`: appended this Prompt 14 entry.

**Result:**
The approved Out of Scope section was applied. No app code or build artifacts
were created.

## Prompt 15 - Review Added Feature Requirements

**Prompt:**
Review Station Comparison Mode and Station Data-Quality Indicator for distinction
from the required app functionality. Identify any extra inputs, calculations,
outputs, and interface changes; recommend implementation in a single-file HTML
app; ask only necessary design questions; do not edit spec.md or write app code.

**Agent Response / Decisions:**
- Confirmed that station comparison is distinct from the required one-at-a-time
  station detail panel because it supports simultaneous selection of up to three
  stations and aligned metric/graph comparison.
- Confirmed that the data-quality indicator is distinct from basic unavailable
  messages because it requires a dedicated diagnostic panel with timestamp, age,
  flags, source, and exclusion reason.
- Identified added inputs: comparison selection state, a maximum of three stations,
  and optional station removal.
- Identified added calculations: no new snowpack formulas; reuse exact-date SWE,
  median, percent-of-median, and water-year series, with separate handling for
  missing/invalid stations.
- Identified added outputs: comparison table and up to three overlaid graph lines,
  plus a data-quality panel with observation metadata and reason text.
- Recommended using existing state variables, data cache, small modal or below-map
  panel, shared chart component, and no separate data-store or build pipeline.
- No spec.md or app code changes were made.

**Files Changed:**
- `prompts.md`: appended this Prompt 15 entry.

**Result:**
Feature planning review completed. User decisions are needed before the Features
section can be finalized.

## Prompt 16 - Add Approved Features Section

**Prompt:**
Approve both additional features and implementation recommendations. Add a
Features section to spec.md for Station Comparison Mode and Station Data-Quality
Indicator, distinguish them from required functionality, document added inputs,
outputs, and calculations, and require implementation only after required
functionality passes validation. Update prompts.md and do not build app code.

**Agent Response / Decisions:**
- Added a Features section to spec.md after Out of Scope.
- Added comparison-mode inputs and outputs: comparison toggle, up to three
  selected triplets, comparison table, shared water-year SWE graph, removal
  controls, and unavailable table rows with omitted graph series.
- Documented reuse of existing SWE, median SWE, and percent-of-median calculations.
- Added the expandable station data-quality panel and all approved diagnostic fields.
- Clarified 24-hour stale handling in current mode and exact-date matching in
  historical mode.
- Clearly separated both features from required app functionality and made them
  dependent on required-feature validation.

**Files Changed:**
- `spec.md`: added the Features section.
- `prompts.md`: appended this Prompt 16 entry.

**Result:**
The approved Features section was added. No app code or build artifacts were
created.

## Prompt 17 - Review Specification and Propose Build Stages

**Prompt:**
Read spec.md carefully, including its seven required sections and two additional
features. Do not write application code. Write a short overview and recommend
4-6 build stages beginning with a page mockup. Each stage must describe what
will be built, what to test, and its completion criteria. Include the interactive
Utah SNOTEL map, NRCS API/SWE calculations, station information/historical SWE
graphs, hand-calculation and NRCS validation, and each additional feature
separately after validation. Do not edit spec.md or index.html; present the plan
for review before implementation.

**Agent Response / Decisions:**
- Read the full specification and AGENTS.md.
- Prepared a six-stage sequence: initial page mockup; interactive Utah map using
  mock data; NRCS API integration, SWE calculations, station information, and
  historical graphs; required-functionality validation; Station Comparison
  Mode; and Station Data-Quality Indicator.
- Kept the two optional features in separate post-validation stages.
- Identified that the current-versus-historical mode boundary and statewide
  eligible-station denominator need to be made explicit before implementation.
- No application files were changed; only this prompt log entry was appended.

**Files Changed:**
- `prompts.md`: appended this Prompt 17 entry.

**Result:**
Planning response prepared for user review. No application code was written,
and spec.md and index.html were not modified.

## Prompt 18 - Add Overview, Clarifications, and Build Stages

**Prompt:**
Approve the six-stage plan and clarify that today in America/Denver is current
mode with the 24-hour stale rule, earlier dates require exact-date observations,
the eligible denominator is every active Utah SNOTEL station with SWE capability,
and the valid numerator includes only stations passing quality, date, and
nonzero-median rules. Add the overview at the beginning, the six stages at the
end with build/test/completion criteria, and record clarifications in the
appropriate sections. Do not build app code. Continue prompt logging and confirm
readiness for Stage 1.

**Agent Response / Decisions:**
- Added an App Overview at the beginning of spec.md.
- Clarified current versus historical mode in Purpose and Inputs.
- Clarified eligible denominator and valid numerator in Inputs and Calculations.
- Added the six approved Build stages, each with what will be built, what to test,
  and completion criteria.
- Gated the two optional features until required functionality passes Stage 4.
- Preserved the pending status of independent NRCS Utah Snow Survey report
  comparisons.
- Did not create or modify index.html or any application code.

**Files Changed:**
- `spec.md`: added the App Overview, clarified current/historical and station
  count rules, and appended Build stages.
- `prompts.md`: appended this Prompt 18 entry.

**Result:**
The specification is ready for Stage 1 planning. No app implementation was
started.

## Prompt 19 - Build Stage 1 Page Mockup

**Prompt:**
Read spec.md and build only Stage 1 as a single-file index.html containing the
page layout with title, date picker, statewide summary, Utah map placeholder,
station details and SWE graph placeholders, marker legend, responsive
engineering-focused styling, accessible labels, and visible keyboard focus.
Use SAMPLE/PLACEHOLDER content only. Do not connect to NRCS, implement
calculations, add custom features, or build later stages. Update prompts.md,
explain browser preview and review checks, and do not commit.

**Agent Response / Decisions:**
- Created a self-contained index.html with inline CSS and minimal JavaScript
  only for the America/Denver date default and future-date maximum.
- Added responsive desktop map/details columns and mobile vertical stacking.
- Added an illustrative Utah map silhouette with clearly labeled sample markers,
  visible five-level marker legend, and gray unavailable swatch.
- Added statewide summary, sample station details, and an SVG graph placeholder,
  with clear notices that all values and marks are non-data placeholders.
- No NRCS requests, real calculations, station interactions, or additional
  features were implemented.
- No commit was created.

**Files Changed:**
- `index.html`: created Stage 1 page mockup.
- `prompts.md`: appended this Prompt 19 entry.

**Result:**
Stage 1 mockup created. Verification and user review remain before approval;
later stages have not been built.

**Verification addendum:**
- Opened index.html in the browser and confirmed the expected accessible page
  structure and placeholder disclosures.
- Checked 390px mobile and 1440px desktop viewports; neither has horizontal
  overflow, and the layout changes from one mobile column to two desktop columns.
- Confirmed the date input defaults to the current America/Denver date and sets
  the same date as its maximum.
- Stage 1 remains pending user visual review and approval.

## Prompt 20 - Build Stage 2 Interactive Map

**Prompt:**
Read the spec and build only Stage 2 in index.html. Replace the map placeholder
with a browser mapping library, center on Utah, enable zoom/pan, add clearly
labeled sample SNOTEL markers with the five-level color scale and gray
unavailable state, legend, marker selection/details, desktop hover and mobile
tap behavior, and keyboard-accessible station selection. Keep the responsive
layout and single-file app, using CDN library resources as needed. Do not call
NRCS, implement real calculations or historical graphs, build Stages 3-6, or
commit. Update this log and test desktop/mobile behavior.

**Agent Response / Decisions:**
- Replaced the illustrative map with Leaflet 1.9.4 and OpenStreetMap tiles;
  no NRCS endpoint or data request was added.
- Added six clearly labeled synthetic mock stations across Utah, including five
  percent-of-median color bands and one gray unavailable marker.
- Added marker hover tooltips, click/tap popups, a keyboard-operable alternative
  station list, and sample details that update when a station is selected.
- Preserved the responsive page, visible legend, sample statewide summary, and
  graph placeholder; no real SWE calculations or custom features were added.
- Browser-tested desktop at 1440px and mobile at 390px: all six markers render,
  marker selection and hover tooltips work, zoom controls change map tiles,
  map dragging pans, keyboard Enter selects a station, mobile tap selection
  updates details, and there is no horizontal overflow.
- Confirmed no AWDB/NRCS endpoint or `fetch()` call is present in index.html.

**Files Changed:**
- `index.html`: replaced the static map placeholder with an interactive
  Leaflet map using sample-only data.
- `prompts.md`: appended this Prompt 20 entry.

**Result:**
Stage 2 interactive map and browser checks completed. Stages 3-6 were not built.
No commit was created; Stage 2 awaits user review and approval.

## Prompt 21 - Build Stage 3 NRCS Data and Station Views

**Prompt:**
Read spec.md and build only Stage 3: retrieve active Utah SNOTEL metadata and
observations from the NRCS AWDB REST API, show real coordinates and SWE,
calculate percent of median and statewide averages, populate station details,
add the water-year SWE graph, apply current/historical and unavailable-data rules,
show loading/error/retry states, preserve the responsive and keyboard layout,
test today's date and April 1, 2025, and do not build Stages 4-6 or commit.

**Agent Response / Decisions:**
- Replaced mock station data with live AWDB metadata and WTEQ observations.
- Loaded 141 active Utah SNOTEL stations with SWE monitoring capability.
- Added chunked exact-date and recent-range AWDB requests, unrounded percent
  calculations, statewide unweighted averaging, valid/eligible coverage, and
  per-station unavailable reasons.
- Added real station details and source links, plus an SVG water-year graph using
  NRCS observations and median values with gaps for missing observations.
- Added loading, NRCS failure, and retry banner behavior; retained the existing
  Leaflet map and responsive/keyboard layout.
- Did not add either custom feature or implement additional build stages.

**Test Outcomes:**
- Confirmed browser CORS and AWDB `access-control-allow-origin: *`.
- Current mode 2026-11-24: 0 valid / 141 eligible. The exact-date request returned
  no observations, and the recent-range response was quality-unapproved or stale.
- Historical mode 2025-04-01: 65 valid / 141 eligible with an unweighted statewide
  average of 95%.
- Brighton: SWE 21.4 inches, median 21.6 inches, displayed percent 99%.
- Snowbird: SWE 38.6 inches, median 36.5 inches, displayed percent 106%.
- Ben Lomond Peak: SWE 33.4 inches, median 33.4 inches, displayed percent 100%.
- Browser-tested the graph and desktop/mobile layouts; no horizontal overflow was
  found at 390px and 1440px widths.
- AWDB daily data does not provide an exact observation-time timestamp, only a
  date. The app therefore labels the timestamp as not provided and uses the
  observation date for the displayed 24-hour age/stale check.

**API and Validation Issues:**
- The exact April 1 and recent-range bulk requests worked, but service limits
  and response size required 35-station batches.
- Today's exact-date request returned no station values, so current-mode
  statewide availability was correctly unavailable rather than fabricated.
- Independent NRCS Snow Survey report comparison remains pending.
- Required Stage 4 validation should not be considered complete until the
  three-station app values and edge cases pass formal tests.

**Files Changed:**
- `index.html`: replaced Stage 2 sample station behavior with Stage 3 AWDB
  metadata, observations, calculations, details, graph, loading, error, and
  retry behavior.
- `prompts.md`: appended this Prompt 21 entry.

**Result:**
Stage 3 implementation and live-data checks were performed. No custom features,
Stage 4 validation, or later stages were added, and no commit was created.

## Prompt 22 - Investigate Hourly AWDB Current Data

**Prompt:**
Investigate why today's view has zero valid stations and whether AWDB offers
hourly SWE suitable for current mode. Preserve historical exact-date daily data,
the 24-hour freshness rule when accurate timestamps exist, explicit provisional
or unavailable status, and real measurements only. Do not change code, start
Stage 4, or commit. Explain findings and recommendation; log this request.

**Agent Response / Decisions:**
- Queried the official AWDB metadata endpoint with Utah SNOTEL, WTEQ, HOURLY,
  activeOnly, and station-element parameters: all 141 active stations advertise
  hourly WTEQ capability.
- Queried hourly WTEQ for the three validation stations. The response includes
  timestamp strings such as `2026-11-24 08:00`, real SWE values, `qcFlag`, and
  `qaFlag`. Metadata's `dataTimeZone` is -8.0 and the OpenAPI schema describes
  this as the station data time-zone offset from GMT.
- The latest hourly values for Brighton, Snowbird, and Ben Lomond Peak were
  `qcFlag=V`, `qaFlag=R`; earlier hourly points also included QA `P`.
- Current daily exact-date request for 2026-11-24 returned zero rows. The
  previous daily date had records, but the latest statuses were not `V/A`.
- The existing strict filter requiring `qcFlag=V` and `qaFlag=A` is consistent
  with spec.md; those flags explain zero valid current observations rather than
  an incorrect division or API parsing issue. Daily reporting also lags the
  current Utah date.
- The daily-only age calculation cannot accurately enforce 24 hours because it
  uses date-only values. Current mode should use hourly timestamps and the
  AWDB timezone metadata; historical mode should retain exact-date DAILY data.
- Hourly responses did not include a 1991-2020 median value. Daily historical
  responses for matching November 24 dates in 2023, 2024, and 2025 did include
  matching AWDB median fields for the three test stations; the daily current-date
  request did not.
- Recommended current mode request HOURLY WTEQ for a bounded recent interval,
  compute age from the returned timestamp and documented AWDB offset, show
  timestamped values younger than 24 hours, and label non-A QA flags explicitly
  as not approved/provisional rather than silently presenting them as confirmed.
- To preserve the approved `qaFlag=A` calculation and statewide inclusion rules,
  provisional hourly SWE should be displayed separately and excluded from
  percent-of-median markers and statewide averages until AWDB marks it accepted.
  Retrieve the official same-calendar-day daily median reference separately;
  never use the hourly observation date/value as a substitute historical daily
  record. If the daily median cannot be obtained, display the median and
  percent-of-median as unavailable.
- No code, spec.md, Stage 4 tests, or commits were changed or started.

**Files Changed:**
- `prompts.md`: appended this Prompt 22 entry.

**Result:**
Hourly AWDB availability and current-data filtering were investigated. The
recommendation is ready for user review; implementation remains unchanged.

## Prompt 23 - Correct Current Mode to Use Hourly AWDB SWE

**Prompt:**
Implement the approved Stage 3 current-data correction. Current mode must use
recent hourly AWDB WTEQ, station `dataTimeZone` and timestamps for the 24-hour
freshness check, show actual Raw/Provisional readings as unapproved while
excluding them from percentage and statewide calculations, and obtain the
1991-2020 median from an AWDB daily median request. Historical mode must remain
exact-date daily with existing quality rules. Preserve the map and historical
graphs; update spec.md and prompts.md, test November 24, 2026 and April 1, 2025,
confirm historical values, and do not start Stage 4, add features, or commit.

**Agent Response / Decisions:**
- Updated the relevant requirements in spec.md for current hourly readings,
  timestamp/time-zone freshness, Raw/Provisional/Approved flag handling, and
  daily same-calendar-day median lookup that never substitutes a prior-year SWE
  value. Historical mode remains exact-date DAILY data with `qcFlag=V` and
  `qaFlag=A`.
- Updated index.html to request current HOURLY WTEQ and the matching daily
  median, calculate age using AWDB's station time-zone offset, display the
  latest actual hourly SWE and timestamp, and exclude unapproved, stale,
  invalid-quality, missing-median, and zero-median readings from percentage
  calculations.
- November 24, 2026 browser test: 140 numeric hourly readings out of 141
  eligible stations; 139 were Raw (`R`) and 1 was Provisional (`P`); all 140
  were within 24 hours; one station had no hourly reading. Zero stations
  qualified for the statewide average, which correctly displayed unavailable.
- Brighton current detail showed an actual 3.1-inch Raw reading, 3.3-inch
  daily median reference, timestamp `2026-11-24 08:00` at AWDB UTC-08:00, and
  unavailable percent-of-median.
- April 1, 2025 historical values remained unchanged: Brighton 21.4/21.6
  inches, 99%; Snowbird 38.6/36.5 inches, 106%; Ben Lomond Peak 33.4/33.4
  inches, 100%. The historical statewide summary remained 65/141 valid and
  95%.
- Browser checks at 390px and 1440px found no horizontal overflow. No browser
  page errors were reported.
- These are Stage 3 behavior checks, not Stage 4 validation. Independent NRCS
  Snow Survey report comparison remains pending; no claim is made that the app
  has passed formal validation.

**Files Changed:**
- `spec.md`: documented the approved current hourly and historical daily
  behavior.
- `index.html`: implemented current hourly retrieval and display, median lookup,
  freshness handling, and approved-quality filtering.
- `prompts.md`: appended this Prompt 23 entry and its test outcome.

**Result:**
The Stage 3 current-data correction was tested for both requested dates, and
historical reference values remained unchanged. Stage 4 and optional features
were not started, and no commit was created.

## Prompt 24 - Stage 4 Required-App Validation

**Prompt:**
Validate Brighton, Snowbird, and Ben Lomond Peak for April 1, 2025 against the
approved AWDB references; independently compare the official NRCS Utah Snow
Survey report; show Brighton's hand calculation; test missing, invalid-quality,
zero-median, stale, and exact-date behavior; confirm Raw/Provisional exclusion
and the unweighted valid-only statewide average; test station selection,
historical graphs, keyboard use, and desktop/mobile layouts. Record expected and
actual values, differences, outcomes, and sources in spec.md. Update this log.
Do not begin Stages 5 or 6, invent data, change calculations without explanation,
or commit.

**Agent Response / Decisions:**
- Browser-checked the April 1, 2025 AWDB reference cases. App results matched
  exactly: Brighton 21.4/21.6 inches and 99%; Snowbird 38.6/36.5 inches and
  106%; Ben Lomond Peak 33.4/33.4 inches and 100%. Each station passed the
  0.1-inch SWE and nearest-whole-percent acceptance criteria.
- Confirmed Brighton's calculation: `(21.4 / 21.6) × 100 = 99.074...%`,
  i.e. 99.07%, displayed as 99%.
- Retrieved the official Utah SNOTEL Snow/Precipitation Update Report for
  April 1, 2025. It is marked provisional and based on the first reading of the
  day (typically 00:00). It reports Brighton 20.8/21.2 inches at 98%,
  Snowbird 37.7/36.3 inches at 104%, and Ben Lomond Peak 33.1/33.3 inches at
  99%. The app-minus-report differences are respectively +0.6/+0.4 inches/+1
  percentage point; +0.9/+0.2 inches/+2 points; and +0.3/+0.1 inches/+1
  point. These comparisons do not match and are not reported as passes. The
  exact cause/convention difference remains unresolved; no calculation was
  changed.
- Controlled in-browser tests of the app's processing/rendering functions
  passed for exact-date-only history, missing prior-day-only data, invalid QC
  and QA flags, zero median, a 30-hour stale reading, and Raw/Provisional
  current observations. Raw/Provisional SWE remains visible with status while
  percent is unavailable and those readings are excluded.
- The unweighted-average fixture with valid percentages 200% and 100% among
  four eligible stations displayed 150% and 2/4, confirming unavailable
  stations do not enter the average.
- The live April 1, 2025 statewide result was 65/141 valid stations with a 95%
  unweighted average; it was not compared with a basin-weighted NRCS statistic.
- Snowbird keyboard selection opened its station details and graph. The graph
  loaded both SWE series. Browser checks at 390px and 1440px found no horizontal
  overflow; no JavaScript errors were reported.
- A controlled stale-reading case found that the summary wording called all
  numeric hourly readings “recent.” Changed this label to “hourly SWE readings”;
  no calculations or eligibility rules changed.
- Updated Validation in spec.md with expected and actual AWDB values,
  differences, the report comparison and source, edge/UI test outcomes, and
  unresolved limitations. Stage 4 is not complete pending review of the
  independent report discrepancy. Stages 5 and 6 were not started.

**Files Changed:**
- `index.html`: corrected the current-summary wording only; calculation behavior
  was unchanged.
- `spec.md`: replaced planned validation language with actual AWDB, official
  report, edge-case, interaction, and layout results plus unresolved issues.
- `prompts.md`: appended this Prompt 24 entry and outcomes.

**Result:**
AWDB reference checks and controlled functional/UI tests passed. Independent
NRCS report comparisons differed for all three stations, so validation remains
unresolved and Stage 4 is not approved complete. No optional stage was started
and no commit was created.

## Prompt 25 - Investigate AWDB and Utah Report Date Alignment

**Prompt:**
Investigate why the April 1, 2025 Utah Snow Survey report differs from the app's
AWDB DAILY values. Verify observation timing, reporting-period and median
conventions, quality flags, whether the app request follows the approved spec,
and recommend preserving or changing retrieval. Explain how to document the
result without claiming unmatched report comparisons passed. Do not edit
spec.md or index.html, commit, or begin Stage 5; update this log only.

**Agent Response / Findings:**
- Queried the official AWDB DAILY WTEQ endpoint for all three triplets on
  2025-04-01 with `centralTendencyType=MEDIAN`, `returnFlags=true`, and both
  `periodRef=END` and `periodRef=START`.
- The app's approved `periodRef=END` request returned:
  - Brighton: 21.4 SWE / 21.6 median, `qcFlag=V`, `qaFlag=A`.
  - Snowbird: 38.6 SWE / 36.5 median, `qcFlag=V`, `qaFlag=A`.
  - Ben Lomond Peak: 33.4 SWE / 33.4 median, `qcFlag=V`, `qaFlag=A`.
- AWDB `periodRef=START` for 2025-04-01 instead returned Brighton 20.8/21.2,
  Snowbird 37.7/36.3, and Ben Lomond Peak 33.1/33.3, all with valid `V/A`
  flags. Those values reproduce the official report's SWE and median values.
- A daily `periodRef=END` request for 2025-03-31 returns those same values as
  `periodRef=START` for 2025-04-01. The API documentation defines `periodRef`
  as choosing the timestamp at the start or end of the observation period.
  Thus, the difference is the daily period boundary/date labeling: the app's
  April 1 END records are the later end-of-period readings, not the report's
  first reading on April 1.
- Queried AWDB HOURLY WTEQ for March 31 through April 1. The April 1 00:00
  readings are exactly the report's current SWE: Brighton 20.8, Snowbird 37.7,
  Ben Lomond Peak 33.1; all three have `qcFlag=V` and `qaFlag=A`.
- The report identifies itself as provisional and says it is based on the
  first reading of the day (typically 00:00). The report's medians also match
  the AWDB `periodRef=START` values. There is no evidence that a different
  median climatology or Raw/Provisional QA flags caused the discrepancies;
  the median changes with the period/date alignment.
- Confirmed the Stage 3 historical code sends exact selected-date DAILY
  requests with `periodRef=END`, `centralTendencyType=MEDIAN`, and
  `returnFlags=true`, then requires exact date plus `qcFlag=V` and `qaFlag=A`.
  This correctly implements the currently approved specification and AWDB
  reference query, but it does not select the report's first-reading
  convention.
- Recommendation: preserve the approved `periodRef=END` calculations and
  AWDB validation baseline until the user approves any change. If the required
  meaning of a selected date is instead the report's first reading at 00:00,
  changing to `periodRef=START` would require revising the validation values,
  historical display, and graph data convention together. Do not present the
  current independent report comparisons as passed against the app's
  `periodRef=END` values.
- Recommended future spec documentation: retain separate AWDB END and report/
  START reference rows; state that the report is provisional and based on
  first daily reading; show the numeric differences and explain that they are
  period-alignment differences; leave independent comparisons marked
  unmatched until the date convention is approved.
- No calculations, index.html, or spec.md were changed. Stage 5 was not begun
  and no commit was created.

**Sources:**
- AWDB data endpoint, queryable with the triplets and dates described above:
  `https://wcc.sc.egov.usda.gov/awdbRestApi/services/v1/data`
- AWDB API documentation, including the `periodRef` definition:
  `https://wcc.sc.egov.usda.gov/awdbRestApi/v3/api-docs`
- Official April 1, 2025 Utah SNOTEL Snow/Precipitation Update Report:
  `https://wcc.sc.egov.usda.gov/reports/UpdateReport.html?report=Utah&year=2025&month=4&day=1`

**Files Changed:**
- `prompts.md`: appended this Prompt 25 investigation and findings.

**Result:**
The mismatch is explained by AWDB daily period-reference alignment, not an
AWDB parsing error or a quality-flag failure. Preserve the approved END-mode
calculation pending user review; the independent report comparison remains
unmatched under that convention. No Stage 5 work or commit was performed.

## Prompt 26 - Plan Historical START-Period Alignment

**Prompt:**
Plan a Stage 4 change to historical daily `periodRef=START` so the app aligns
with the official Utah Snow Survey report. Identify required updates to
historical daily requests, SWE/median graphs, April 1 validation cases,
Brighton's hand calculation, and the Calculations and Validation sections.
Do not modify current-mode hourly handling, index.html, or spec.md yet. Explain
risks and whether the independent report comparisons would pass. Update this
prompt log only; do not commit or begin Stage 5.

**Agent Response / Findings:**
- Confirmed the April 1, 2025 official report's provisional first-reading
  values match AWDB DAILY `periodRef=START` and the AWDB HOURLY values at
  `2025-04-01 00:00`:
  - Brighton: 20.8 inches SWE, 21.2 inches median, 98%.
  - Snowbird: 37.7 inches SWE, 36.3 inches median, 104%.
  - Ben Lomond Peak: 33.1 inches SWE, 33.3 inches median, 99%.
  The matching AWDB START and hourly records have `qcFlag=V` and `qaFlag=A`.
- Confirmed the app currently sends `periodRef=END` for historical daily
  station requests, historical graph requests, and station source links. These
  must be changed to START together to keep station values, both graph series,
  and source URLs aligned.
- The April 1, 2025 expected validation values should become the report/START
  values above. Brighton's hand calculation should become
  `(20.8 / 21.2) × 100 = 98.113...%`, or 98.11%, displayed as 98%.
- Calculations documentation should define the historical DAILY convention as
  START-of-period and continue using same-record SWE and 1991-2020 median,
  unrounded for percent calculations. Validation should record the revised
  triplet references, query with `periodRef=START`, exact report source,
  provisional/first-reading convention, flags, and explicit app-vs-report
  results after implementation and testing. Build-stage descriptions and
  station-source links should be checked for matching historical convention.
- The existing AWDB `periodRef=END` data and prior app behavior should be
  retained as the old baseline/audit context, not silently relabeled as a
  START result. Changing conventions will alter historical displayed SWE,
  medians, percentages, statewide summaries, and graph values. Daily gaps,
  exact-date matching, quality checks, and unrounded formulas remain unchanged.
- The historical change does not require changing current-mode HOURLY WTEQ
  retrieval, timestamps, `dataTimeZone`, freshness, or Raw/Provisional handling.
  However, current mode separately retrieves a DAILY median for the matching
  calendar day. Using END there may preserve the old median period convention;
  using START would align that median with the selected report-date convention
  but can change current-mode percentages, so this required a separate user
  decision.
- User decision: use `periodRef=START` for the current-mode DAILY median lookup
  too, while leaving the HOURLY WTEQ request and its timestamp, freshness, and
  quality handling unchanged.
- Based on direct AWDB results, using START for the historical SWE and median
  records is expected to make all three April 1 station comparisons match the
  official report values and nearest-whole-percent results. This is a
  prediction from source data, not a passed app test; formal comparisons must
  be rerun after implementation.
- No code, specification, calculations, or current-mode handling were changed.
  Stage 5 was not begun and no commit was created.

**Files Changed:**
- `prompts.md`: appended this Prompt 26 planning entry and findings.

**Result:**
The historical START-period change is scoped and expected to align the three
validation stations with the official report. The user also approved START for
the current-mode DAILY median lookup while keeping the HOURLY request unchanged.
No implementation was started.

## Prompt 27 - Implement Historical START Alignment

**Prompt:**
Implement the approved Stage 4 alignment in index.html and spec.md: use DAILY
`periodRef=START` for historical station data, historical graph series, and
historical source links; also use START for the current-mode DAILY median
lookup without changing HOURLY SWE handling. Update validation references,
Brighton's hand calculation, Calculations, and Stage 3/4 descriptions. Retest
the app against AWDB START and the official report, including current data,
graphs, average, keyboard, and responsive layouts. Update prompts.md. Do not
add custom features, begin Stage 5, or commit.

**Agent Response / Changes:**
- Updated the data request helper to accept a period reference. Historical
  daily station data and both SWE/median graph series now request START.
  Historical station source links also use START.
- Current-mode daily median lookup now requests START. The current HOURLY WTEQ
  request remains HOURLY with its existing END reference; timestamp,
  `dataTimeZone`, freshness, and quality handling were unchanged.
- Updated spec.md Calculations, historical Inputs/Purpose, Validation, and
  Stage 3/4 descriptions to define the START convention. Previous END values
  are retained only as historical context.
- Browser-tested April 1, 2025 against live AWDB START data and the official
  Utah report:
  - Brighton: app 20.8 / 21.2 in, 98%; report 20.8 / 21.2 in, 98%.
  - Snowbird: app 37.7 / 36.3 in, 104%; report 37.7 / 36.3 in, 104%.
  - Ben Lomond Peak: app 33.1 / 33.3 in, 99%; report 33.1 / 33.3 in, 99%.
  All differences were zero and each comparison met the 0.1-inch SWE and
  nearest-whole-percent criteria.
- Brighton hand calculation is `(20.8 / 21.2) × 100 = 98.113...%`, or 98.11%,
  displayed as 98%.
- The April 1 live statewide result under START was 71/141 valid and 92%.
  The earlier END run was 65/141 and 95%; the formula was not changed.
- Historical graphs loaded both series for all three stations. Browser request
  inspection confirmed historical station, graph, and source-link requests use
  START. The current median request uses DAILY START, while hourly data requests
  remain HOURLY END.
- Current regression on November 24, 2026: 140 hourly values (139 Raw, 1
  Provisional, 1 station with no reading), 0/141 valid. Brighton remained
  3.1-inch Raw SWE at 2026-11-24 08:00, percent unavailable; its daily START
  median was 3.4 inches. The hourly request/QA behavior was unchanged.
- Rechecked exact-date missing, invalid QC/QA, and zero-median fixtures; each
  remained unavailable as required. Keyboard selection opened station details
  and graphs; 390px/1440px layouts had no horizontal overflow. No browser
  errors were reported.
- The independent report comparisons pass for these three April 1 cases. The
  report remains provisional and can be revised upstream; the results are
  specific to the retrieved report.
- Stage 5 and the two optional features were not started; no commit was made.

**Files Changed:**
- `index.html`: applied START to historical DAILY requests, graph requests,
  historical source links, and current-mode DAILY median lookup; hourly SWE
  handling remains unchanged.
- `spec.md`: updated the START convention, validation values/results, hand
  calculation, and Stage 3/4 descriptions.
- `prompts.md`: appended this Prompt 27 entry and test outcomes.

**Result:**
The three AWDB START and official report comparisons matched exactly in the
live app. The requested Stage 4 alignment checks passed; the report's
provisional status remains a limitation. No Stage 5 work or commit was

## Prompt 28 - Build Stage 5 Station Comparison Mode

**Prompt:**
Implement only Stage 5 in index.html: add an accessible Station Comparison Mode
toggle, select up to three SNOTEL stations, show their SWE, median, percent,
and data availability in a table, and overlay their water-year SWE series on
a shared graph with a clear legend. Prevent a fourth selection, allow removals,
keep unavailable stations in the table but omit unavailable graph series, and
preserve normal single-station mode. Reuse the validated AWDB data and rules,
keep the START historical convention and current hourly behavior unchanged,
do not build Stage 6, update prompts.md, test desktop/mobile and requested
selection cases, and do not commit.

**Agent Response / Changes:**
- Added a clearly labeled, keyboard-operable Station Comparison Mode checkbox.
  Map markers and the accessible station list can add or remove stations; the
  app rejects a fourth station with a live status message. Each table row has
  an accessible Remove button.
- Added a responsive comparison table with station, SWE, median SWE, percent
  of median, availability explanation, and removal action.
- Added a shared water-year SWE graph. It uses daily AWDB WTEQ with
  `periodRef=START`, approved QC/QA observations, readable axes, gaps for
  missing records, station-specific colors and line styles, and a text legend.
  A station whose selected-date observation fails the applicable date, quality,
  or current freshness rules remains in the table but has its graph series
  omitted with an explanation.
- Comparison mode reuses already processed SWE, median, percent, and status
  values; no calculation formula or current-mode hourly request was changed.
  Turning the mode off restores the prior single-station panel and selection.
  Comparison selections are retained if the user later turns the mode back on.
- Added responsive horizontal scrolling for the comparison table on narrow
  screens, semantic table headers/caption, a labeled scroll region, keyboard
  controls, and visible focus styling.
- Corrected the statewide mode label during API failures to reflect the
  last-successfully-loaded dataset, rather than the newly requested date. The
  existing last-known-data warning and Retry behavior remain in place.
- Updated the Stage 5 status in spec.md and the app's stage labels. Stage 6 was
  not started.

**Test Results:**
- Comparing one, two, and three stations passed: table row counts and shared
  graph line counts were 1/1, 2/2, and 3/3.
- April 1, 2025 comparison values matched the approved Stage 4 references:
  Brighton 20.8/21.2 in, 98%; Snowbird 37.7/36.3 in, 104%; Ben Lomond Peak
  33.1/33.3 in, 99%.
- Attempting a fourth station left the count at three and announced the limit.
  Removing a station reduced the comparison and graph series as expected.
- Clarkston Mountain's exact-date-missing record remained in the table with
  SWE, median, and percentage unavailable; its graph series was omitted while
  the two valid series remained. An invalid-QC station was also retained with
  its quality explanation and omitted from the graph.
- Current-mode regression showed Brighton's Raw reading (3.1 in SWE, 3.4 in
  median, percent unavailable) with the Raw QA explanation and no graph line.
  Raw/Provisional readings remain excluded from accepted graph series.
- Switching between normal and comparison modes restored Brighton's normal
  details and graph without changing its values.
- At 390px, the page had no horizontal overflow and the 650px comparison table
  scrolled within its 326px viewport. At 1440px, map and comparison panels
  remained side by side with no page overflow.
- A transient NRCS fetch failure preserved and clearly labeled last-known data;
  Retry succeeded and the historical comparison loaded. A forced-failure
  browser check confirmed the displayed mode matched the last-loaded data.
- Browser page-error checks were clear and `git diff --check` passed. Node.js
  was unavailable for a standalone syntax check; the updated inline script
  loaded and executed in the browser.

**Files Changed:**
- `index.html`: implemented Stage 5 comparison UI, station selection/removal,
  table, shared graph, and mode display correction.
- `spec.md`: recorded Stage 5 as implemented and awaiting user review.
- `prompts.md`: appended this Prompt 28 entry and test results.

**Result:**
Stage 5 comparison behavior and requested browser checks passed. The transient
NRCS failure recovered with Retry. Stage 6 remains unstarted; no commit was
made.

## Prompt 29 - Build Stage 6 Station Data-Quality Indicator

**Prompt:**
Implement only Stage 6 in index.html: add an expandable accessible data-quality
panel inside station details with observation date/time/age, AWDB QC and QA
flags and meanings, median availability, source and station identifier,
effective status, and a plain-language acceptance/exclusion explanation.
Reuse current 24-hour and historical exact-date rules, preserve formulas,
periodRef=START, current hourly handling, and Station Comparison Mode. Test
historical/current flags, missing observation/median, stale and invalid data,
date and mode switching, and desktop/mobile. Update prompts.md, update Stage 6
status in spec.md only after testing, and do not commit.

**Agent Response / Changes:**
- Added a native expandable Station Data Quality section in the selected
  station details panel. It reports observation date, exact hourly timestamp
  with AWDB UTC offset, current observation age, qcFlag, qaFlag, median
  availability, station triplet, official AWDB request link, effective status,
  and a plain-language explanation.
- QA meanings are shown as R = Raw, P = Provisional, and A = Approved. QC
  displays its returned value and explains that the app accepts only V.
- Effective status uses the existing processed station status and values:
  Valid, Missing, Invalid, Stale, or Median unavailable. The panel distinguishes
  historical daily records without an exact time from missing exact-date data.
- The panel uses existing status, timestamps, quality flags, age, median, and
  percentage fields. No SWE formulas, period references, hourly retrieval, or
  quality filters were changed. Comparison mode still hides and restores the
  normal station view without losing the selected station's panel state.
- Updated the Stage 6 status in spec.md after testing.

**Test Results:**
- Approved historical Brighton (April 1, 2025) showed Valid, exact date,
  qcFlag V, qaFlag A, a 21.2-inch median, and the accepted-calculation
  explanation. Its AWDB source URL retained `periodRef=START`.
- Current Brighton Raw (`R`) and Louis Meadow Provisional (`P`) observations
  showed their actual timestamps, AWDB UTC-08:00 offsets, age, median
  availability, and exclusion explanations.
- Clarkston Mountain's exact-date-missing record showed Missing with no
  observation date/timestamp or flags claimed. Agua Canyon's invalid qcFlag E
  showed Invalid. Atwater's historical record had SWE but no median and showed
  Median unavailable. Agua Canyon on August 1, 2025 showed a zero median and
  the percent-undefined explanation.
- A controlled browser-clock check used Brighton's actual hourly AWDB reading
  while advancing only the browser clock; at 48.7 hours old it showed Stale
  and explained the 24-hour exclusion.
- Date changes between historical/current modes, keyboard expansion, and
  comparison-mode on/off passed. The panel was open/readable at desktop and
  mobile widths; at 390px the page had no horizontal overflow and the quality
  grid collapsed to one column.
- An attempted route-fulfilled synthetic missing-median test timed out while
  the intercepted request was pending. It was replaced by the live Atwater
  historical case with an unavailable median, which exercised the panel's
  missing-median state using official AWDB data.
- Browser execution of the updated page succeeded and `git diff --check`
  passed. No persistent automated test suite was added.

**Files Changed:**
- `index.html`: added the Stage 6 quality panel, flag explanations, effective
  status text, and responsive styles.
- `spec.md`: recorded Stage 6 implementation and test outcomes after testing.
- `prompts.md`: appended this Prompt 29 entry and results.

**Result:**
Stage 6's requested data-quality states and integration checks passed. The
route-based synthetic fixture was unnecessary after the live missing-median
case passed. No commit was made.
performed.

## Prompt 30 - Final Pre-publication Audit

**Prompt:**
Read AGENTS.md, spec.md, index.html, and prompts.md. Audit all six stages,
placeholders, links/resources, JavaScript and network errors, HTTP/API/CORS and
GitHub Pages compatibility, April 1, 2025 validation cases, graphs and both
features, Data Quality visibility, responsive/keyboard/date behavior, personal
identifiers, single-file architecture, and final specification contents.
Report passed checks, problems, publishing risks, and remaining requirements.
Do not make major changes or edit code without approval. Record this audit and
do not commit or publish.

**Agent Response / Findings:**
- Read all four requested project files. All six stages are implemented in the
  app and documented, including the three validation cases, Brighton hand
  calculation, actual results, Features section, and stage-by-stage build plan.
- Served the app over local HTTP. The page returned HTTP 200; live AWDB
  metadata/current observations and historical data loaded in-browser. A valid
  AWDB data GET returned HTTP 200 with `Access-Control-Allow-Origin: *`.
  The bare data endpoint without required query parameters returned HTTP 400,
  as expected; the official report redirected and resolved to HTTP 200.
- The browser reported no JavaScript console errors, failed requests, or
  unsuccessful resource responses during the HTTP audit. HTTPS Leaflet CDN,
  official AWDB endpoints, OSM copyright, and Leaflet project links responded.
- April 1, 2025 app results matched the documented values:
  Brighton 20.8/21.2 inches, 98%; Snowbird 37.7/36.3 inches, 104%; Ben Lomond
  Peak 33.1/33.3 inches, 99%. All three historical graph series loaded with
  `periodRef=START`; the comparison view showed three rows, graph series, and
  legend entries.
- Selecting Brighton showed and keyboard-expanded the Data Quality panel with
  Valid status, `qcFlag=V`, `qaFlag=A`, and the exact-date acceptance reason.
  At current date 2026-11-24, the app loaded 140 hourly readings, all
  unapproved, with 0/141 valid and the statewide average unavailable, as
  expected for the returned flags.
- Date selection set the max to today's America/Denver date. Keyboard station
  selection, native details expansion, 390px mobile layout, and 1440px desktop
  layout were checked; neither viewport had horizontal page overflow.
- No personal name, NetID, or email identifier was found in index.html,
  spec.md, or prompts.md. The application remains a single index.html with
  Leaflet/CSS/JS and map tiles loaded over HTTPS; the repository has four
  tracked top-level files, including its documentation.
- Issues needing review: the initial unselected graph still renders two
  hard-coded curves instead of a clearly empty/loading state; the header and
  footer still identify the interface as “Stage 5” although Stage 6 is
  implemented; and the Validation status paragraph says Stages 5 and 6 have
  not begun, contradicting their implementation statuses.
- Publishing risks: no GitHub Pages deployment has been tested. AWDB availability
  and CORS remain dependent on NRCS service behavior; the public OSM tile service
  is best-effort and subject to its usage policy. A direct curl tile probe was
  denied, while the actual browser loaded Leaflet tiles without failed requests.
  The independent report remains provisional and subject to revision.
- No calculations or application code were changed. Small corrections to the
  initial graph, stage labels, and stale specification sentence are awaiting
  user approval.

**Files Changed:**
- `prompts.md`: appended this Prompt 30 audit and results.

**Result:**
The live HTTP audit passed for API access, validation values, graphs, both
features, accessibility interactions, and responsive layouts. The three
identified content inconsistencies remain unmodified pending user approval.
No commit or publication was made.

### Prompt 30 Follow-up - Approved Audit Corrections

**User Decision:**
- Approved the focused corrections to the initial graph, visible stage labels,
  and stale specification status.

**Changes and Retests:**
- Removed the two hard-coded initial SWE graph curves and placeholder y-axis
  values. Before station selection, the graph now identifies itself as having
  no selected station and asks the user to select one; no fabricated series is
  shown.
- Removed “Stage 5” from the live-data header and footer.
- Updated the Validation status to acknowledge Stages 5 and 6 are implemented,
  and removed the obsolete Stage 5 text that said Stage 6 remained gated.
- Retested over local HTTP: the page loaded; current data returned 0/141 valid
  with 140 hourly readings marked unapproved; the empty graph had zero data
  paths before selection.
- April 1, 2025 again matched all three references: Brighton 20.8/21.2 in,
  98%; Snowbird 37.7/36.3 in, 104%; Ben Lomond Peak 33.1/33.3 in, 99%.
  Historical graphs loaded two data paths each and source links used START.
- Keyboard expansion of the Brighton Data Quality panel passed. Three-station
  comparison showed three table rows, graph series, and legend entries.
  At 390px and 1440px, page width matched viewport width.
- No browser console errors, failed requests, or failed responses were observed.
  `git diff --check` passed.

**Files Changed:**
- `index.html`: removed fabricated initial graph curves, clarified its empty
  state, and removed stale visible stage labels.
- `spec.md`: corrected the obsolete Stage 4 and Stage 5 status prose.
- `prompts.md`: appended this audit follow-up.

**Result:**
The approved corrections passed the HTTP browser retests. No calculations,
AWDB request behavior, or quality rules changed. The app remains unpublished
and uncommitted; GitHub Pages deployment has not been tested.

## Prompt 31 - Investigate GitHub Pages AWDB Failures

**Prompt:**
Investigate why the deployed GitHub Pages app reports an AWDB HTTP 403 while
localhost works. Inspect all AWDB requests, identify the failing endpoint,
compare URL parameters, Origin, Referer, and response headers, assess blocking,
rate limiting, hosting-origin restrictions, metadata versus observations, and
recommend a reliable solution preserving live official NRCS data, single-file
HTML, and GitHub Pages. Do not use an untrusted proxy, hard-code measurements,
change calculations, or edit app code. Update this log and wait for approval
before changes.

**Agent Response / Findings:**
- Identified the deployed site as
  `https://brayallen.github.io/utah_snowpack_map/` from the repository remote;
  it serves the app over HTTPS.
- Inspected all AWDB routes in index.html:
  - First-load metadata: `GET /stations` with wildcard Utah SNOTEL triplets,
    WTEQ, DAILY, `activeOnly=true`, and `returnStationElements=true`.
  - Current mode: five 35-station HOURLY WTEQ batches (`beginDate=-24`,
    `endDate=0`, `periodRef=END`) and five DAILY median batches for the prior
    matching calendar day (`periodRef=START`, `centralTendencyType=MEDIAN`).
  - Historical mode: DAILY exact-date WTEQ batches with START and median.
  - Station and comparison graphs: DAILY WTEQ requests with START.
- Could not reproduce the reported HTTP 403. The deployed page returned HTTP
  500 on the metadata endpoint in one load and HTTP 500 on a current-mode DAILY
  median batch in a later load. Because metadata failed first in the first
  attempt, no observation request followed that failure. In the later attempt,
  the metadata request had succeeded before the median batch failed.
- The same GitHub Pages-origin browser later fetched metadata, one-station
  current HOURLY SWE, and one-station DAILY median successfully (HTTP 200).
  The exact 35-station median batch that had returned 500 subsequently returned
  HTTP 200 with both GitHub and localhost Origin/Referer values.
- Localhost browser requests used the same API host, methods, Accept header,
  URLs, and parameters. Captured requests had no Origin header in either
  browser; Referer was `http://127.0.0.1:8000/` locally and
  `https://brayallen.github.io/` on the deployed page. Curl requests with
  explicit GitHub and localhost Origin/Referer headers both returned HTTP 200.
- Failed responses were from the NRCS Apache/mod_jk server and included
  `Access-Control-Allow-Origin: *` and `Access-Control-Allow-Headers: *`.
  The captured HTTP 500 responses had an empty body and no `Retry-After` header.
  Successful localhost responses used the same server and permissive CORS
  headers.
- The evidence does not support a GitHub Pages CORS or origin restriction.
  Browser code received an HTTP response, so this is not a browser CORS failure.
  No rate-limit status/header was observed; rate limiting cannot be confirmed.
  Intermittent AWDB-side/server errors are the best-supported explanation, but
  the user's reported 403 cannot be assigned to a specific endpoint without
  its Network-panel request details. The app currently reports only the status,
  not which request failed.
- Recommendation: make no proxy, header-spoofing, endpoint, calculation, or
  data-source change. The direct official API requests work from both origins.
  If failures recur, capture the failing request URL/status/headers from the
  published page. A repeatable 403 should be referred to NRCS AWDB support;
  a static GitHub Pages app has no supported same-origin proxy mechanism.
  If approved later, improve resilience with bounded retry/backoff for
  transient 429/5xx responses (honor `Retry-After`) and include the endpoint
  role in the error message; do not retry or bypass a 403 automatically.
- No application code, validated formulas, reporting conventions, or API
  parameters were changed. No third-party proxy or sample data was used.

**Files Changed:**
- `prompts.md`: appended this Prompt 31 investigation and recommendations.

**Result:**
The published-site 403 was not reproducible during the audit. Two transient 500
responses occurred at different request stages, while the same endpoints and
exact failed batch subsequently returned 200 from both hosting contexts.
Evidence points away from a GitHub Pages origin restriction; the intermittent
upstream failure and the reported 403's precise request remain unconfirmed.
No commit or publication change was made.

## Prompt 32 - Add Bounded AWDB Retries

**Prompt:**
Add up to three total attempts with exponential backoff for AWDB HTTP 429 and
5xx responses, honor Retry-After within a maximum delay, never retry 403, show
the failed endpoint and status, preserve last-successful data with a warning,
and limit excessive requests. Preserve all validated calculations and data
conventions. Test temporary, persistent, and successful requests on localhost;
update spec.md and prompts.md; do not commit; explain GitHub Pages publication
and verification steps.

**Investigation / Decision Needed:**
- Confirmed AWDB browser responses currently expose `Access-Control-Allow-Origin`
  and `Access-Control-Allow-Headers`, but not `Access-Control-Expose-Headers`.
  `Retry-After` is not a CORS-safelisted response header, so a GitHub Pages
  script cannot read it unless NRCS exposes it on the response.
- A client-only implementation can parse and honor `Retry-After` when the
  response makes it readable, and otherwise apply bounded exponential backoff.
  It cannot guarantee honoring a header that the browser's CORS rules hide.
- No application code or spec changes have been made pending the user's
  decision whether this best-effort client-only behavior is acceptable or
  whether to pause for an NRCS-supported way to expose that header.

**Files Changed:**
- `prompts.md`: appended this request and the CORS limitation.

**Result:**
Implementation and the requested retry tests are paused for clarification.

### Prompt 32 Follow-up - Approved Best-Effort Retry and Verification

**User Decision:**
- Approved the client-only best-effort approach: read `Retry-After` when the
  browser exposes it, otherwise use bounded exponential backoff.

**Changes and Test Outcomes:**
- Implemented the approved retry and request-serialization behavior in
  `index.html`, and documented its CORS limitation and unchanged data rules in
  `spec.md`.
- Browser-tested a simulated HTTP 429 with an exposed `Retry-After: 1`: the
  retry occurred after about 1.0 seconds, then the data load completed
  successfully. Five data batches plus the retried first batch produced six
  requests.
- Browser-tested a persistent HTTP 503: exactly three attempts were made, the
  user-facing warning identified `/data (DAILY WTEQ)` and HTTP 503, and the
  last successful station data remained displayed.
- Browser-tested HTTP 403: exactly one request was made, with no automatic
  retry; the warning identified `/data (DAILY WTEQ)` and HTTP 403 and retained
  the last successful data.
- Browser-tested recovery through a successful mocked response and confirmed
  the live localhost app then loaded official NRCS data. For April 1, 2025,
  Brighton remained 20.8 inches SWE, 21.2 inches median, and 98%; statewide
  coverage was 71/141 with a 92% unweighted average.
- Delayed intercepted requests across 25 AWDB calls and measured a maximum of
  one simultaneous request, confirming serialization.
- `git diff --check` passed. No validated calculation or observation rule was
  changed.

**Files Changed:**
- `index.html`: bounded retry, request serialization, and last-known-data
  reliability behavior.
- `spec.md`: documented the reliability behavior and CORS limitation.
- `prompts.md`: appended this approval and verification record.

**Result:**
The approved reliability improvement passed the simulated 429, persistent 503,
non-retryable 403, recovery, serialization, and live localhost validation
checks. The browser-only `Retry-After` limitation remains: a header hidden by
NRCS CORS cannot be read by the app. No commit or publication was made.