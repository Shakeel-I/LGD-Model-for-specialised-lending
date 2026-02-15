# LGD Model for Specialised Lending  
**Aerospace & Project Finance – Service-Style Technical Overview**

<img width="614" height="461" alt="image" src="https://github.com/user-attachments/assets/e7eb135e-ff30-435b-91f1-ebb8a930a2d3" />

## 1. Purpose and scope

This document outlines a specialised **Loss Given Default (LGD)** framework for Aerospace and Project Finance exposures, designed to be deployable as an analytical service or model component within a bank's credit risk infrastructure. It demonstrates compliance with regulatory, governance and credit-committee expectations for internal LGD solutions.

The framework combines a Zero-One Inflated Beta (ZOIB) statistical model with explicit regulatory floors, conservative overlays and structured documentation outputs. It supports point-in-time and regulatory LGD estimation, stress testing and transaction-level credit assessment.

## 2. Core methodology

The LGD model uses a ZOIB specification to accommodate the empirical features of specialised lending recoveries:

- Boundary mass at 0 and 1 to capture full recovery and total loss events explicitly.  
- A Beta-distributed component on the open interval (0, 1) for partial recoveries.  
- A three-part likelihood function estimated via non-linear optimisation.

**Key risk drivers:**
- Seniority and security package (priority ranking, collateral type and coverage)  
- Leverage and collateralisation (LTV, haircuts)  
- Asset quality tiering (Tier 1 vs Tier 3 aerospace hulls, core vs non-core infrastructure)  
- Resolution time and workout complexity (legal costs, enforcement processes)  
- Macroeconomic variables (GDP growth), enabling downturn calibration  

Parameter estimates include t-values and p-values, retaining drivers that are both economically intuitive and statistically robust (p < 0.05 where feasible).

## 3. Defence Dossier concept

Model outputs form a standardised **"Defence Dossier"** for credit committee papers or validation reviews, organised around four pillars:

### Pillar 1 – Statistical Evidence
Parameter estimates, significance metrics, goodness-of-fit indicators and rank-ordering statistics.

### Pillar 2 – Directional Reasoning
Economic explanations of driver impacts:
- **Seniority**: higher seniority ? lower LGD  
- **Resolution time**: longer periods ? higher LGD (legal/carry costs, discounting)  
- **GDP growth**: stronger growth ? lower LGD (downturn consistent)  

### Pillar 3 – Asset Specialisation
Differentiation between Aerospace and Project Finance, asset tiers, jurisdictions and data-scarcity safeguards (35% LDP floor for project finance).

<img width="614" height="461" alt="image" src="https://github.com/user-attachments/assets/1f6d01f4-bb99-4e67-95f0-61ab09b1578e" />


### Pillar 4 – Discriminatory Power
Spearman rank correlations across portfolios/segments showing higher-risk exposures receive higher LGDs.

## 4. Illustrative transaction: Project Finance

**"Project Helios"** (Infrastructure/Renewables):

| Parameter | Value |
|-----------|-------|
| Asset class | Project Finance |
| EAD | £150m |
| Seniority | Senior secured |
| LTV | 72% |
| Asset quality | Tier 1 (PPA-backed) |

**Model results:**
- **Point-in-time LGD**: 28.4%  
- **Regulatory LGD** (post-MoC/stress): 42.6%  

The regulatory LGD incorporates 3.5-year resolution horizon, 10% MoC and 35% LDP floor, producing a conservative yet economically coherent outcome for a senior, high-quality infrastructure asset.

## 5. Implementation and analytical pipeline

Designed for standard analytical stacks (SAS or equivalent):

**Non-linear estimation**
- High-dimensional ZOIB likelihood optimisation (NEWRAP-type algorithms)
- Stable convergence on complex likelihood surfaces

**Data integration**
- Facility-level (seniority, collateral, guarantees)
- Asset-level qualitative indicators (tier, jurisdiction)
- Macroeconomic time series (GDP)

**Validation**
- Rank-ordering and correlation statistics
- Bimodal density plots and residual diagnostics

**Deployment options:** Managed analytics service or hosted risk platform component.

## 6. Regulatory and governance alignment

**PRA SS11/13**: 9% discount rate floor, downturn LGD treatment  
**PRA SS1/23**: Structured "reasoned argument" documentation, transparent MoC  
**PRA PS1/26 / Basel 3.1**: 25% unsecured corporate floor, 35% project finance LDP floor  

Governance artefacts support internal model approval, validation and regulatory dialogue.

## 7. Theoretical and industry foundations

- **Caselli, S., Gatti, S., & Querci, F. (2008)**. "The Determinants of Loss Given Default (LGD) on Business Loans: An Empirical Analysis."  
- **Gatti, S. (2018)**. "Project Finance in Theory and Practice."  
- **UK PRA SS1/23** – Model risk management principles for banks.  
- **BCBS d424** – "Regulatory Treatment of Specialised Lending."




.
