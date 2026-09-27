# Swirltubs Aftermarket Service Inventory Optimization

## Project Overview

This project develops a data-driven inventory stocking strategy for **Swirltubs**, an appliance manufacturer with a warranty service network of approximately **1,000 field technicians**.

Technicians carry replacement parts in their service vans. The business faces a trade-off between maintaining enough inventory to complete repairs on the first visit and controlling inventory holding costs, limited van capacity, and technician revisit costs.

The project evaluates optimization and heuristic-based stocking strategies and uses stochastic simulation to test inventory decisions under uncertain technician-level demand.

## Business Problem

Swirltubs currently allows technicians to manage their own van inventory, resulting in inconsistent stocking decisions.

When a required part is unavailable:
1. The technician orders the part from the central warehouse.
2. The technician must return to the customer after the part arrives.
3. Additional technician time and travel are incurred.
4. Customer service performance decreases.

The objective is to determine a practical stocking strategy that balances inventory holding cost, technician revisit cost, van storage capacity, part demand, and first-visit repair performance.

## Dataset

The analysis uses approximately **416 frequently used parts**, representing about 80% of typical annual repair activity.

Each part includes:
- Part Number
- Annual / average usage
- Part Cost
- Part Size in cubic feet

The full model uses a **500 ft³ van capacity constraint**.

## Methodology

### 1. Optimization Model

A binary inventory optimization model was developed to determine whether each part should be stocked. The model considers inventory holding cost, expected revisit cost, part size, and available van capacity.

### 2. Jenkins Threshold Model

A rule-based approach was evaluated using:
- Usage > 1
- Cost < $70
- Size < 8 ft³

### 3. Heuristic Model

A cost-efficiency heuristic was developed to balance the benefit of stocking a part against the amount of van space it consumes.

```text
(Revisit Cost − Inventory Cost) / Part Size
```

Parts were ranked according to their score and selected until available capacity was reached.

### 4. Stochastic Simulation

Because part failures are uncertain and demand can vary between technicians, the model was tested using **100 randomized demand scenarios** based on historical usage.

Each scenario evaluated:
- Parts selected
- Inventory cost
- Revisit cost
- Total cost
- First-visit success rate
- Van capacity utilization

## Results

### 30-Part Test Dataset

| Model | Parts Selected | Space Used | Estimated Cost | First-Visit Success |
|---|---:|---:|---:|---:|
| Optimization Model | 7 | 49.98 ft³ | $1,556.14 | 21% |
| Jenkins Model | 10 | 47.76 ft³ | $875.57 | 40% |
| Heuristic Model | 16 | 40.81 ft³ | $686.26 | 67% |

### Full Dataset

| Metric | Result |
|---|---:|
| Parts Selected | **213** |
| Van Space Used | **494.60 ft³** |
| Inventory Cost | **$3,566.91** |
| Revisit Cost | **$10,712.99** |
| Total Cost per Van | **$14,279.90** |
| First-Visit Success Rate | **46.64%** |

## Key Insights

- **Cost vs. service:** Minimizing inventory cost alone can increase return visits when important parts are unavailable.
- **Demand uncertainty:** Historical average demand does not fully capture technician-level variation, making simulation useful for evaluating stocking strategies.
- **Heuristic approach:** A practical heuristic can provide a scalable alternative when full optimization becomes difficult to implement.
- **Capacity utilization:** The final heuristic used approximately **494.6 ft³ of the available 500 ft³**.

## Recommendations

- Use the optimization model as a cost-effectiveness benchmark.
- Use the heuristic model as an operational stocking approach.
- Pilot the stocking strategy with a smaller group of technicians.
- Monitor first-visit success, revisit frequency, inventory cost, and technician feedback.
- Preserve some van capacity for technician-specific requirements.
- Refresh the stocking strategy using updated demand data.
- Integrate the stock list with inventory and replenishment systems.
- Continue testing the model under unusual demand scenarios.

## Tools & Skills

- Microsoft Excel
- Optimization Modeling
- Binary Integer Programming
- Inventory Optimization
- Supply Chain Analytics
- Heuristic Modeling
- Stochastic Simulation
- Scenario Analysis
- Data Analysis
- Operations Research
- Business Analytics

## Repository Structure

```text
Swirltubs-Inventory-Optimization/
│
├── README.md
├── Case Study Problem Statement.pdf
├── Case Study Report.pdf
└── Case Study Final Model.xlsm
```

## Project Deliverables

- **Case Study Problem Statement.pdf** — Original business problem and analytical requirements.
- **Case Study Report.pdf** — Analysis, methodology, results, and recommendations.
- **Case Study Final Model.xlsm** — Excel-based optimization, heuristic, and simulation model.

## Project Context

This project is based on the **Swirltubs After Market Product Inventory and Service** case study from the University of Dayton. The case requires an optimization model, comparison of heuristic approaches, and application of the selected strategy to the full dataset.

## Author

**Pranav Nangare**

Graduate Student | Data Analytics | Business Intelligence | Supply Chain Analytics
