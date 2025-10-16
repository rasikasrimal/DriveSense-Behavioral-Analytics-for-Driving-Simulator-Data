# DriveSense-Behavioral-Analytics-for-Driving-Simulator-Data

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
