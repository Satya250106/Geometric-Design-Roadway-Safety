# Technical Report
## Geometric Design and Safety Analysis of Roadways

**Project type:** Academic transportation engineering project  
**Period stated in project materials:** March–April 2026  
**Prepared for:** Portfolio documentation  
**Status:** Technical review required before design conclusions are claimed

## 1. Executive summary

Four supplied spreadsheets were organized into a reproducible repository covering (i) four-legged intersection signal timing, (ii) design traffic and axle-repetition estimation, (iii) axle-load damaging-effect calculations, and (iv) rigid pavement fatigue-damage calculations. Selected input/output tables and illustrative charts are included for faster review.

The workbook structure is useful as an academic calculation portfolio. However, the formula audit identified open items that affect the reliability of some outputs. In particular, flexural-stress formulas in the fatigue worksheet appear to reference different input cells in successive rows, and the displayed total fatigue damage appears to sum only the BUC block even though a separate TDC block exists. These items must be resolved before reporting a final pavement-fatigue conclusion.

## 2. Scope and source files

| Source workbook | Organized repository path | Main subject |
|---|---|---|
| `Assignment 5-1.xlsx` | `calculations/traffic-signal-design/traffic-signal-timing-four-legged-intersection.xlsx` | Approach flows, saturation flows, critical flow ratios, cycle and green time |
| `Cls 3.xlsx` | `calculations/rigid-pavement-design/design-traffic-calculations.xlsx` | Traffic growth, design traffic, axle repetitions, day/night splits |
| `Transportation design practice.xlsx` | `calculations/axle-load-analysis/axle-load-damaging-effect.xlsx` | Fourth-power damaging-effect examples |
| `TDC and BUC Calculations-1.xlsx` | `calculations/rigid-pavement-design/design-axle-and-fatigue-damage.xlsx` | Design axle calculations and rigid pavement fatigue worksheet |

The project title mentions geometric design and safety analysis. The supplied workbooks do not clearly document superelevation, transition curves, sight distance, or horizontal/vertical alignment. Those topics should be added only when source calculations or field records are available.

## 3. Methods represented in the workbooks

### 3.1 Design traffic

The workbook uses a cumulative traffic-growth expression of the form:

`N = 365 × (((1 + r)^n − 1) / r) × A`

where `r` is the annual growth rate, `n` is design life in years, and `A` is the initial daily traffic term defined in the workbook. The value `r = 0.075` is entered. Confirm that this means 7.5% per year and that the traffic definition is consistent across all related workbooks.

### 3.2 Axle-load damaging effect

The workbook uses a fourth-power relationship of the form:

`D = (W / Wref)^4`

where `W` is the axle load and `Wref` is the reference load specified by the chosen method. Reference loads vary between formula blocks in the source workbook. Their basis must be verified before comparing the calculated damage values or citing a design standard.

### 3.3 Traffic signal timing

The signal workbook records approach widths and traffic volumes for northbound, southbound, eastbound, and westbound approaches. It estimates saturation flow, computes volume-to-saturation-flow ratios, selects critical ratios, and allocates effective green time. The displayed phase green times should be reconciled with the effective green time and with lost-time, amber, and all-red assumptions.

### 3.4 Rigid pavement fatigue

The fatigue worksheet includes material and support inputs, a trial slab thickness, axle-load classes, load frequencies, expected repetitions, flexural stress, stress ratio, allowable repetitions, and fatigue-damage summation. The source contains separate calculation blocks for BUC and TDC traffic conditions. Formula references and aggregation logic need to be checked before interpreting the total.

## 4. Extracted data and illustrative figures

The repository includes:
- `data/processed/traffic-signal-approach-data.csv`
- `data/processed/design-traffic-inputs-and-cached-outputs.csv`
- `visualizations/traffic-volume-by-approach.png`
- `visualizations/illustrative-axle-damaging-effect.png`

The CSVs are selected extracts from workbook inputs and cached outputs. They are included for review and visualization, not as independently verified design values.

## 5. Technical quality-assurance findings

| ID | Priority | Finding | Required action |
|---|---|---|---|
| QA-01 | Critical | Flexural-stress formulas appear to use shifting condition references, e.g. successive rows test different cells such as B5, B6, and B7. | Trace every row formula to the intended equation and fixed input references. |
| QA-02 | Critical | The displayed total fatigue damage formula sums H65, H80, and H95, corresponding to the left-hand block, while a TDC block appears on the right. | Confirm intended reporting and calculate a separate TDC total if required. |
| QA-03 | High | Phase-green calculations sum to approximately 39.6 s while the workbook shows effective green time of 41 s. | Reconcile lost time, phase allocation, rounding, amber, and all-red assumptions. |
| QA-04 | High | Growth rate is entered as 0.075 with a label that mentions percent. | Explicitly document 7.5%/year and ensure consistent use as a decimal fraction. |
| QA-05 | High | The damaging-effect workbook uses different reference loads in different formula blocks. | Verify the intended standard, axle configuration, and reference load for each block. |
| QA-06 | Medium | Axle proportions and lateral placement adjustment require definition checks. | Confirm proportions total 1.0 where expected and document factor meaning. |
| QA-07 | Medium | Units, calculation references, and input/output conventions are not fully standardized. | Add units, standards, assumptions, version date, and input/formula formatting. |
| QA-08 | Scope | Geometric alignment calculations were not identifiable in the supplied spreadsheets. | Add evidence or narrow the stated project scope. |

Full machine-readable register: `technical-qa-register.csv`.

## 6. Recommended validation workflow

1. Preserve the original workbooks and make an audit copy.
2. Identify the source textbook/IRC/MoRTH standard for each equation and record the exact edition and clause.
3. Check input units and percentage conventions.
4. Audit formulas row-by-row, paying particular attention to relative versus absolute references.
5. Recalculate the workbook in Excel or another compatible spreadsheet engine.
6. Independently calculate a representative sample of each method.
7. Compare independent results with workbook outputs and document differences.
8. Only after checks pass, create a results table with verified values and engineering interpretation.

## 7. Limitations

- The spreadsheet outputs have not been independently certified.
- The CSV files contain selected cached values; spreadsheet formulas may recalculate differently in a compatible spreadsheet engine.
- No construction-ready design recommendation is made.
- The exact design standards and clauses must be confirmed from the actual course/reference material.
- Additional geometry and field-measurement records are required to substantiate the full resume project scope.

## 8. Conclusion

The supplied workbooks provide a useful base for a transportation-engineering portfolio, particularly in traffic signal timing, traffic-growth calculations, axle-load damage, and rigid pavement fatigue. The repository is structured for transparent review. Final technical conclusions should be added only after the open formula and assumption checks are closed and documented.
