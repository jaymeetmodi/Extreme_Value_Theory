# Modelling Extreme Rainfall in Vadodara Using Extreme Value Theory (Peaks Over Threshold)

An M.Sc. Statistics seminar project that fits a Generalized Pareto Distribution (GPD) to the upper tail of daily rainfall at Bodeli station, Vadodara district, and estimates tail probabilities and return levels.

---

## Overview

Rare, heavy rainfall events drive flood and water-management risk, but ordinary models of the whole distribution describe the tail poorly. Extreme Value Theory (EVT) models the tail directly. This project uses the **Peaks Over Threshold (POT)** method:

```
daily rainfall → high threshold → exceedances → excesses → GPD → tail probability / return level
```

POT uses every observation above the threshold, rather than only one maximum per block as in the block-maxima (GEV) approach.

## Data

| Item | Detail |
|---|---|
| Source | Central Water Commission (CWC) manual daily rainfall data, National Water Data Portal |
| Station | BODELI, Vadodara district, Gujarat |
| Period | 15 June 2014 – 18 October 2020 |
| Processing | Multiple timestamped records on the same date are summed to daily totals |
| Size | **536** recorded calendar-day totals (range 0.2–437.4 mm) |

The record is incomplete: not every calendar day has an observation. The analysis therefore does not treat it as a continuous daily series, and return periods are expressed in numbers of observations rather than years.

## Method

1. Aggregate timestamped records to daily totals.
2. Choose a threshold using the mean residual life plot and parameter-stability plots (**u = 50 mm**).
3. Compute excesses over the threshold (80 exceedances).
4. Fit a GPD to the excesses (`scipy.stats.genpareto`, location fixed at 0).
5. Estimate tail probabilities, return periods and return levels.
6. Check the fit with a GPD Q–Q plot.

## Results

| Measure | Value |
|---|---|
| Threshold | 50 mm |
| Exceedances | 80 of 536 (14.93%) |
| Mean excess | 46.90 mm |
| Shape parameter ξ | 0.1555 (positive, so a heavy tail) |
| Scale parameter β | 39.62 mm |
| P(rainfall > 100 mm) | 0.0472 |
| P(rainfall > 150 mm) | 0.0178 |
| P(rainfall > 200 mm) | 0.0076 |
| Return period, 100 mm | ≈ 21 observations |
| Return period, 150 mm | ≈ 56 observations |
| Return period, 200 mm | ≈ 131 observations |
| Return level, 365 observations | ≈ 270 mm |
| Return level, 7,300 observations | ≈ 551 mm (strong extrapolation, highly uncertain) |

## Limitations

- The station record is short and incomplete.
- Rainfall is seasonal and may be temporally dependent; neither is modelled here.
- Return levels at long horizons extrapolate far beyond the observed data.

The project is intended to demonstrate the POT–GPD workflow rather than to give a full hydrological risk assessment.

## Tools

Python (pandas, NumPy, SciPy, Matplotlib)

## References

- Coles, S. (2001). *An Introduction to Statistical Modeling of Extreme Values.* Springer.
- Kratz, M. – work on EVT and tail risk modelling, as cited in the seminar report.
