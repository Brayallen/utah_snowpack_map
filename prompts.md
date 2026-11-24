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