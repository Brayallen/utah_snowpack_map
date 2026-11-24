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