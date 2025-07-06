# 🚗 Smart Urban Parking Pricing with Pathway

A real-time dynamic pricing engine for urban parking lots based on real-time demand, traffic, and queue data. Built using [Pathway](https://pathway.com/) for scalable stream processing and [Bokeh](https://docs.bokeh.org/en/latest/) + [Panel](https://panel.holoviz.org/) for interactive visualizations in notebooks.

---

## 📌 Project Overview

Urban cities face increasing traffic congestion and inefficient parking usage. This project aims to:

- Dynamically price parking slots based on demand patterns.
- React to real-time features like occupancy, traffic, and queue length.
- Encourage smarter parking choices through competitive pricing.
- Visualize parking prices over time with a live dashboard.

---

## 🛠 Tech Stack

| Tool / Library        | Role                                |
|-----------------------|-------------------------------------|
| **Pathway**           | Real-time data streaming & logic    |
| **Python**            | Main language                       |
| **Pandas**            | For debugging and snapshots         |
| **Panel**             | Interactive UI for Colab/Jupyter    |
| **Bokeh**             | Plotting time-series parking prices |
| **Google Colab**      | Dev & experiment environment        |
| **Mermaid.js**        | Architecture diagrams               |


---

## 🧠 Models Implemented

### ✅ Model 1: Baseline Dynamic Pricing

**Pricing Formula:**

price = 10 + (occ_max - occ_min) / cap

- **occ_max / occ_min**: Peak and lowest occupancy in a daily tumbling window
- **cap**: Max parking capacity
- Encourages pricing based on volatility in demand

### ✅ Model 2: Demand-Based Dynamic Pricing

**Demand Score Calculation:**

Demand = α*(Occupancy/Capacity)+ β . QueueLength - γ . TrafficConditionNearby + δ . IsSpecialDay + ε . VehicleTypeWeight

- All values normalized
- Score clipped between 0 and 1
- **Final Price**:

Price_t = BasePrice * (1 + λ * NormalizedDemand)


This model responds more sensitively to real-time features and simulates business intelligence.

---

## 📊 Architecture Diagram

> 📝 **Note:** If you're viewing this on GitHub and the flowchart below isn't rendering,  
> you might need to [install the Mermaid Live Preview extension](https://marketplace.visualstudio.com/items?itemName=vstirbu.vscode-mermaid-preview)  
> (for VS Code), or use a tool like [Mermaid Preview](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid).

```mermaid
flowchart TD
    A[CSV Replay / Real-Time Feed] --> B[Pathway Streaming Ingest]
    B --> C[Timestamp Parsing & Feature Enrichment]
    
    C --> D1[Model 1: Daily Window Aggregation & Price]
    C --> D2[Model 2: Real-Time Demand Score & Dynamic Price]
    
    D1 --> E[Unified Output Table]
    D2 --> E

    E --> F[📈 Panel + Bokeh Dashboard]
    E --> G["🛠 Debug Snapshots via Pandas"]




