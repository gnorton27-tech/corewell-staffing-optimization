# Corewell Health — Phase 1 Staffing Optimization

Educational multi-objective optimization of 100 **synthetic** hospital staffing scenarios. Not actual Corewell Health data or clinically validated patient safety estimates.

## Objectives
- Minimize modeled staffing cost per 12-hour shift (USD).
- Maximize an **unvalidated modeled safety proxy** (0–100).

## Contents
- `optimization_engine.ipynb`: reproducible data validation, Pareto calculation, dominated examples, five strategies, and three-panel chart.
- `data/staffing_scenarios.csv`: 100 synthetic scenarios (fixed RNG seed 42).
- `data/strategy_comparison.csv`: five strategic selections.
- `images/`: generated figures.
- `requirements.txt`: dependencies.

## Run
From repository root: `pip install -r requirements.txt`, then `jupyter notebook optimization_engine.ipynb`; choose Kernel > Restart & Run All.

## Synthetic data provenance
Generated with NumPy RNG seed 42 and the prompt: “Generate 100 reproducible synthetic hospital staffing scenarios for a classroom multi-objective optimization exercise, with regular/overtime/agency nurses, 12-hour shifts, demand hours, modeled costs, and a clearly labeled unvalidated safety proxy. Use fixed random seed 42; do not represent figures as actual Corewell Health data.”
Assumed hourly rates: regular $48, overtime $72, agency $95 (not verified Corewell rates). Regular nurses 7–15; overtime nurses 0–6; agency nurses 0–5; demand 70–110 nursing hours. Modeled proxy: `clip(100*(1-exp(-1.3*min(available_hours/demand_hours,2.5))) - 1.5*overtime_nurses - 0.8*agency_nurses,0,100)`. No actual patient outcomes were used.

## Method
Scenario A dominates B if A has no higher cost and no lower proxy, with at least one strict improvement. Five frontier-only strategies: balanced equal-weight normalized objectives, smallest objective-score gap, lowest cost, highest proxy, and 60% safety / 40% cost. Objective gap is **not demographic equity**.

## Findings and limitations
Run the notebook to see counts, examples, comparison table, and charts. Synthetic inputs and an unvalidated proxy mean results are illustrative only. Real deployment requires verified costs, patient outcomes, acuity, labor rules, staffing constraints, and clinical review.

## Development commits (suggested)
1. Initialize repository and notebook.
2. Add synthetic dataset and validation.
3. Implement Pareto analysis and strategy comparison.
4. Add figures, documentation, and dependencies.
