# Production Simulation with STC Control Chart

A discrete-event simulation comparing two production strategies using **SimPy**, with **STC (Statistical Throughput Control)** control chart visualization.

---

## 📋 Overview

This project simulates a production environment to evaluate and compare two strategies for meeting a production quota within a fixed time window:

- **Manpower Strategy** — Add extra workers at a specified time point
- **Overtime Strategy** — Keep a fixed workforce and allow overtime beyond the normal shift

Results are analyzed using Monte Carlo simulation (1,000 runs) and visualized with STC control charts.

---

## 🚀 Features

- ✅ Discrete-event simulation via SimPy
- ✅ Monte Carlo analysis (completion rate & production ratio)
- ✅ Cost calculation with 1.5× overtime pay
- ✅ Extrapolated finish-time estimation when quota is not met within `R` hours
- ✅ STC control chart with 5 control lines (z = −1.675 to 1.675)
- ✅ Annotated charts showing key simulation results

---

## ⚙️ Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| `R` | 9.8 hrs | Total simulation duration |
| `quota` | 27,541 units | Production target |
| `prod_mean` | 235 units/hr | Mean output per worker per hour |
| `prod_variance` | 11 | Variance of output per worker per hour |
| `wage` | $20.00/hr | Hourly wage per worker |
| `initial_workers` | 11 | Starting number of workers |
| `T_add` | 2.4 hrs | Time point to add manpower |
| `additional_workers` | 2 | Number of workers added |
| `n_worker` | 11 | Fixed workers for overtime strategy |
| `mu` | 27,541 | STC control line μ parameter |
| `sigma` | 980 | STC control line σ parameter |

---

## 🔄 Program Flow

```
Set Parameters
     │
     ▼
Monte Carlo Simulation (1,000 runs)
     ├── Manpower Strategy → Completion Rate + Avg Production Ratio
     └── Overtime Strategy → Completion Rate + Avg Production Ratio
     │
     ▼
Single Run Comparison (seed = 42, same random sequence for both strategies)
     │
     ▼
Cost Calculation (normal pay + 1.5× overtime)
     │
     ▼
Print Report + Plot STC Control Charts (with result annotations)
```

---

## 💰 Cost Model

**Manpower Strategy**
- Initial workers: normal wage up to `R` hrs; 1.5× beyond `R`
- Additional workers: hired from `T_add`, normal wage up to `R`; 1.5× beyond `R`

**Overtime Strategy**
- All workers: normal wage up to `R` hrs; 1.5× beyond `R`

---

## 📊 STC Control Chart

The **Statistical Throughput Control (STC)** chart plots the **difference between actual and planned cumulative production** over time, overlaid with control lines at z = −1.675, −0.674, 0, 0.674, 1.675.

Control line formula:

```
x(t) = -((μ - Q) × (R - t) / R) - z × σ × √((R - t) / R)
```

---

## 📦 Dependencies

```bash
pip install simpy numpy matplotlib pandas openpyxl
```

---

## ▶️ Usage

```bash
python production_simulation.py
```

Output includes:
1. Monte Carlo statistics (completion rate, avg production ratio)
2. Single-run cost comparison
3. Two STC control charts (one per strategy)

---

## 📁 Project Structure

```
├── production_simulation.py   # Main simulation script
└── README.md
```
