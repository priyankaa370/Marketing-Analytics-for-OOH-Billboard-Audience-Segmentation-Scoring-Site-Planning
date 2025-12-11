# Marketing Analytics for OOH Billboard Planning

## Feature Engineering

As part of the broader effort to score billboards by audience type, this step focuses on transforming the raw dataset into clean, meaningful features that can feed into our audience indices and segmentation logic.

The goal of this feature engineering stage is simple:
**turn raw traffic, demographic, and POI data into signals that actually describe who sees each billboard.**

This can be understood stepwise as follows -
1. Standardizing Percentage Fields

    The dataset contains several percentage columns (age groups, gender share, student share, peak-hour traffic, etc.) stored inconsistently as either 0–1 or 0–100.
    We normalize all of them to a 0–1 scale so the calculations downstream behave correctly.

2. Creating Vehicle Mix Features

    Raw vehicle counts are converted into percentage shares by dividing each count by the total number of vehicles:
    - Car share
    - Bike share
    - Bus share
    - Truck share

    These shares help describe audience type:
    cars often indicate higher income, bikes often indicate youth, buses reflect commuting patterns, and trucks point toward industrial activity.

    This step creates behavioral context rather than relying on plain counts.

3. Encoding Income Groups

    Income categories (Low → Affluent) are mapped to numeric values (1–5).
    This enables income to be used in mathematical formulas when building indices like the AffluenceIndex.

4. Normalizing Core Inputs

    Traffic, POI counts, income levels, and vehicle shares are normalized into a common 0–1 scale so they can be combined fairly.

    This avoids bias where large numbers (like daily traffic) would overpower smaller but meaningful signals (like school density).

5. Building Audience-Specific Signals

    Using the cleaned and normalized features, intermediate signals are created such as:

    - commute_vehicle_mix (cars + buses)
    - pedestrian_norm
    - schools_norm
    - malls_norm
    - factories_norm
    - income_norm

  **These engineered features are later used to calculate the four audience indices (WorkingPro, Student, Affluence, BlueCollar).**
  This engineering step does not assign segments yet—it simply prepares the ingredients.
  Now every billboard has:
  
  - standardized demographic features
  - normalized POI indicators
  - engineered vehicle mix patterns
  - numeric socio-economic indicators

