# 🚗 DriveSense – Driving Simulator Performance Analysis

**DriveSense** is a Python-based analytical toolkit designed to process and evaluate **driving simulator data**.  
It provides automated performance insights across key behavioral metrics such as lane-keeping, speed control, steering activity, and hazard response time.  

This project is intended for **data scientists, simulation researchers, and behavioral analysts** who need to quantify driver performance in controlled environments.

---

## 🧠 Project Overview

The driving simulator generates two primary data files per scenario:

1. **Simulator Output (.xlsx)** – A time-series log of the driver's behavior  
   Contains timestamped records of:
   - Position coordinates (X, Z)
   - Speed
   - Steering angle
   - Timestamps

2. **Infrastructure Data (.csv)** – Spatial map of the driving environment  
   Contains:
   - Feature type (tunnels, bridges, potholes, etc.)
   - Feature coordinates
   - Hazard event markers

The goal is to **combine and analyze** these datasets to extract KPIs and identify performance differences across **specific rule-based driving segments**.

---

## 🧩 Key Features

- **Automated Data Ingestion & Cleaning:**  
  Imports and synchronizes simulator and infrastructure data using **Pandas** and **NumPy**.
  
- **Comprehensive KPI Computation:**  
  - Standard Deviation of Lateral Position (SDLP)  
  - Mean Speed and Speed Variance  
  - Steering Reversal Rate  
  - Lane Exceedances  
  - Hazard Reaction Time  

- **Rule-Based Segment Analysis:**  
  Dynamically defines segments such as:
  - ±100m around tunnels or bridges  
  - ±20m around specific hazards  
  - First-to-last feature occurrences (e.g., pothole field)  
  - Segments between paired objects (e.g., billboard sets)

- **Configurable Analysis Engine:**  
  Parameters like thresholds, segment distances, and event filters can be easily modified in the configuration block.

- **Readable Output Reports:**  
  Results are printed to the console and optionally saved as `.csv` or visualized.

---

## 🧱 Project Structure

```

DriveSense/
│
├── data/
│   ├── scenario_1/
│   │   ├── simulator_output.xlsx
│   │   └── infrastructure.csv
│   └── scenario_2/ ...
│
├── src/
│   ├── data_loader.py          # Load & preprocess input files
│   ├── metrics.py              # KPI computation functions
│   ├── segment_analysis.py     # Rule-based segment definition
│   ├── visualization.py        # (Optional) plotting utilities
│   ├── utils.py                # Helper functions (e.g., distance, filtering)
│   └── main.py                 # Main execution script
│
├── notebooks/
│   ├── exploratory_analysis.ipynb
│   └── demo_run.ipynb
│
├── results/
│   ├── scenario_1_summary.csv
│   └── visualizations/
│
└── README.md

````

---

## ⚙️ Installation

### **1. Clone the Repository**
```bash
git clone https://github.com/yourusername/drivesense.git
cd drivesense
````

### **2. Create a Virtual Environment**

```bash
python -m venv venv
source venv/bin/activate       # Mac/Linux
venv\Scripts\activate          # Windows
```

### **3. Install Dependencies**

```bash
pip install -r requirements.txt
```

### **4. Verify Installation**

Run the sample analysis:

```bash
python src/main.py --scenario data/scenario_1
```

---

## 📦 Dependencies

Main libraries used:

* **Pandas** – Data manipulation and analysis
* **NumPy** – Numerical computations
* **Matplotlib / Seaborn** – (Optional) visualization
* **OpenPyXL** – Read Excel (.xlsx) files
* **argparse / pathlib** – Command-line arguments and path management

Install them manually (if needed):

```bash
pip install pandas numpy matplotlib seaborn openpyxl
```

---

## 🧮 Key Performance Metrics

| Metric                          | Description                               | Formula/Approach                                                                   |
| ------------------------------- | ----------------------------------------- | ---------------------------------------------------------------------------------- |
| **SDLP**                        | Standard Deviation of Lateral Position    | Measures lane-keeping ability by analyzing deviation in lateral position (Z-axis). |
| **Speed Variance & Mean Speed** | Consistency of longitudinal control       | Calculated using rolling mean and variance functions.                              |
| **Steering Reversal Rate**      | Frequency of steering direction changes   | Count sign changes in steering angle data.                                         |
| **Lane Exceedances**            | Number of times driver leaves lane bounds | Compare lateral position vs. lane threshold.                                       |
| **Hazard Reaction Time**        | Delay between hazard trigger and braking  | Timestamp difference between event and response.                                   |

---

## 🧭 Segment Analysis Rules

| Segment Type        | Rule Definition                                        |
| ------------------- | ------------------------------------------------------ |
| **Tunnel / Bridge** | ±100m from start and end coordinate                    |
| **Single Event**    | ±20m around feature (e.g., merging traffic)            |
| **Pothole Field**   | Between first and last occurrence of “pothole” feature |
| **Billboard Pair**  | Between the average X-coordinates of two billboards    |

All rules are defined in `segment_analysis.py` and can be edited or extended.

---

## 🧰 How It Works

1. **Load Data:**
   Simulator `.xlsx` and Infrastructure `.csv` are read into Pandas DataFrames.

2. **Clean & Synchronize:**

   * Remove duplicates and NaNs
   * Normalize timestamps
   * Align datasets based on coordinates or time

3. **Calculate KPIs:**
   Compute SDLP, speed metrics, and steering behavior using vectorized operations.

4. **Segment Analysis:**
   Dynamically detect regions of interest based on spatial rules and calculate KPIs per segment.

5. **Summarize & Export:**
   Print formatted metrics to console and optionally export `.csv` summary.

---

## 🧩 Example Output

```
Scenario: Bridge Test

Overall KPIs
---------------------------------
Mean Speed: 73.4 km/h
Speed Variance: 12.1
SDLP: 0.24 m
Steering Reversal Rate: 0.83 per sec
Lane Exceedances: 3
Hazard Reaction Time: 1.43 s

Segment Analysis: Tunnel Zone (100m before & after)
---------------------------------
Mean Speed: 69.7 km/h
SDLP: 0.18 m
Lane Exceedances: 0
```

---

## 🧑‍💻 Developer Notes

* Ensure timestamps are consistent between both input files.
* SDLP can be sensitive to coordinate scaling; verify your simulator’s unit system (meters vs pixels).
* For hazard events, define the brake threshold (e.g., speed drop > 5 km/h within 2s).
* You can extend metrics by adding new functions under `metrics.py`.

---

## 🧱 Future Enhancements

* **Geospatial Visualization:** Display trajectories using Folium or Plotly.
* **Comparative Analysis:** Evaluate multiple drivers/scenarios statistically.
* **Automated Reports:** Export PDF or HTML summaries.
* **Machine Learning Insights:** Predict unsafe driving patterns using anomaly detection.

---

## 🧾 License

MIT License © 2025 Your Name
Free to use, modify, and distribute with attribution.

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository
2. Create a new branch
3. Submit a pull request with clear documentation

---

## 📧 Contact

For questions, feedback, or collaboration:
**Email:** [yourname@example.com](mailto:yourname@example.com)
**LinkedIn:** [linkedin.com/in/yourprofile](https://linkedin.com/in/yourprofile)

---

```

---

Would you like me to make this README **auto-tailored to your personal developer brand** (for example, adding your GitHub, LinkedIn, and short “About Me” section at the end)? It makes a big difference when you attach it to an Upwork proposal or GitHub portfolio.
```


Phase 1 – Data Understanding & Architecture Design

Goal: Build a clear understanding of input structure and define the analytical pipeline.
Tasks:

Review the simulator .xlsx and infrastructure .csv schemas.

Identify key variables: timestamps, positions (X, Z), steering, speed, event types.

Design a modular code structure for data loading, processing, and metric calculation.

Plan class/function design for maintainability (e.g., DriveAnalyzer, FeatureMapper).

Deliverable:
A well-documented project skeleton or Jupyter Notebook outline showing planned structure.

Phase 2 – Data Ingestion & Cleaning

Goal: Ensure both input files are accurately loaded and synchronized by time.
Tasks:

Use Pandas to import and merge .xlsx (simulator) and .csv (infrastructure) files.

Handle missing or duplicated timestamps, outliers, and coordinate inconsistencies.

Align both datasets via timestamps or distance interpolation.

Convert raw data into unified dataframes ready for analysis.

Deliverable:
Cleaned and merged dataset with validation checks.

Phase 3 – Core KPI Computation

Goal: Implement core behavioral metrics for driver performance.
Tasks:

SDLP (Standard Deviation of Lateral Position): Compute from lateral deviations.

Speed Variance & Mean Speed: Derive from longitudinal data.

Steering Reversal Rate: Detect sign changes in steering angle data.

Lane Exceedances: Identify deviations beyond a defined lateral threshold.

Hazard Reaction Time: Measure delay between hazard events and braking activity.

Deliverable:
Python functions producing overall performance metrics with Pandas/Numpy vectorization.

Phase 4 – Segment Definition & Rule-Based Analysis

Goal: Build logic for advanced, rule-based segment detection.
Tasks:

Define start and end points dynamically for:

±100m around tunnels/bridges

±20m windows around single events

Ranges from first to last instance of a repeated feature (e.g., pothole field)

Average position-based segments (e.g., between billboard sets)

Create reusable helper functions for segment extraction.

Run metric calculations within each segment context.

Deliverable:
Automated segment creation system with per-segment KPI summaries.

Phase 5 – Results Aggregation & Visualization

Goal: Summarize results clearly and provide visual insights.
Tasks:

Aggregate results into summary tables (overall + per segment).

Visualize trends with Matplotlib/Seaborn (optional but impactful).

Print results neatly formatted to console (for .py file).

Add an export option (e.g., CSV summary).

Deliverable:
Readable output report or console summary with visual verification plots (if enabled).

Phase 6 – Optimization, Testing & Documentation

Goal: Finalize the project for reusability and scalability.
Tasks:

Parameterize file paths and thresholds for reusability on new datasets.

Write docstrings and inline comments.

Test across the four scenarios for performance and accuracy.

Optionally package as a command-line or notebook tool.

Deliverable:
Clean, reusable, and well-documented final Python script or notebook.

✅ Optional Phase 7 – Extensions (for Ongoing Work)

Add geospatial visualization with Folium/Plotly for route replay.

Integrate statistical comparison across drivers or sessions.

Automate report generation in PDF or HTML format.

Implement anomaly detection for unsafe driving patterns.
