# Marketing Analytics for OOH Billboard Planning

## Feature Engineering

As part of the broader effort to score billboards by audience type, this step focuses on transforming the raw dataset into clean, meaningful features that can feed into our audience indices and segmentation logic.

The goal of this feature engineering stage is simple:
**turn raw traffic, demographic, and POI data into signals that actually describe who sees each billboard.**

This can be understood stepwise as follows -
**1. Standardizing Percentage Fields**

The dataset contains several percentage columns (age groups, gender share, student share, peak-hour traffic, etc.) stored inconsistently as either 0–1 or 0–100.
We normalize all of them to a 0–1 scale so the calculations downstream behave correctly.

**2. Creating Vehicle Mix Features**

Raw vehicle counts are converted into percentage shares by dividing each count by the total number of vehicles:
- Car share
- Bike share
- Bus share
- Truck share

These shares help describe audience type:
cars often indicate higher income, bikes often indicate youth, buses reflect commuting patterns, and trucks point toward industrial activity.

This step creates behavioral context rather than relying on plain counts.

**3. Encoding Income Groups**

Income categories (Low → Affluent) are mapped to numeric values (1–5).
This enables income to be used in mathematical formulas when building indices like the AffluenceIndex.

**4. Normalizing Core Inputs**

Traffic, POI counts, income levels, and vehicle shares are normalized into a common 0–1 scale so they can be combined fairly.

This avoids bias where large numbers (like daily traffic) would overpower smaller but meaningful signals (like school density).

**5. Building Audience-Specific Signals**

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

## Index Calculation

Each index represents how strongly a billboard location aligns with a specific audience segment.

Each site receives four scores, each normalized on a 0–100 scale for easy interpretation.

**1. WorkingProIndex (Working Professionals)**

**Purpose: Identify locations strong for office-going commuters.**
This index combines demographic and mobility signals that typically represent working professionals:

- Share of working professionals in the nearby population
- Commute vehicle mix (cars + buses)
- Number of offices within 1 km
- Overall traffic volume

Billboards with a high WorkingProIndex are ideal for **B2B brands, banking, insurance, office supplies, fintech, productivity products, and weekday commuter campaigns.**

**2. StudentIndex (Youth & Students)**

**Purpose: Identify locations dominated by youth/students.**
This score captures the lifestyle and movement patterns of younger audiences:

- Student population share
- Share of individuals aged 15–24
- Proximity to schools and colleges
- Pedestrian activity (hangout zones, campuses, markets)
- Evening peak traffic

High-scoring sites are suitable for **fashion, QSR brands, education services, gaming, entertainment, and youth-centric promotions.**

**3. AffluenceIndex (Affluent Shoppers & Professionals)**

**Purpose: Measure the economic strength and spending capacity around each site.**
Affluence is inferred using:

- Local income levels (numericized from income segment)
- Mall density (premium retail clusters)
- Presence of offices (white-collar employment)
- Car ownership share (proxy for higher income)
- Concentration of the 25–44 age group (peak earning years)

This index is essential for luxury retail, real estate, automobile brands, premium FMCG, and high-value product launches.

**4. BlueCollarIndex (Industrial & Workforce Zones)**

**Purpose: Identify industrial corridors and blue-collar dominated regions.**
The score is built using:

- Blue-collar population share
- Factories within 3 km
- Truck share in traffic mix
- Off-peak activity (night shift movements)

High-scoring sites are relevant for **logistics brands, tools & equipment, beverages, fast-moving mass-market products, and industrial recruitment.**

**5. Normalization (0-100 Scale)**

All raw index formulas are finally scaled using min–max normalization:
        
        Index = (value - min) / (max - min) * 100
Normalization ensures that scores are comparable across all cities, tiers, and traffic patterns so that marketers can instantly understand relative strength. Additionally, percentile rankings and segment tagging remain consistent.
