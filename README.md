# nyc-taxicab-eda
# NYC Taxicab Operations — Exploratory Data Analysis

Exploratory Data Analysis on 2023 NYC Yellow Taxi trip data to uncover 
patterns that can inform strategic decisions on routing, pricing, and 
passenger experience.

---

## Objective

To analyse 2023 NYC Yellow Taxi trip records and derive actionable insights 
that help optimise taxi operations — specifically around fleet deployment, 
zone-level demand patterns, revenue maximisation, and pricing strategy.

---

## Dataset

- **Source:** NYC Taxi & Limousine Commission (TLC)
  https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
- **Period:** January 2023 – December 2023 (12 monthly parquet files)
- **Raw size:** ~3 million trips per month
- **Sampled size:** ~1.83 million trips (5% stratified sample per hour per date)
- **Format:** Parquet → sampled to CSV for analysis

---

## Tools and Libraries

- Python 3.12
- Pandas 2.2.2
- NumPy 2.0.2
- Matplotlib 3.10.0
- Seaborn 0.13.2
- GeoPandas 1.1.3

---

## Project Structure

nyc-taxicab-eda/

├── nyc_taxicab_eda.ipynb   ← Main analysis notebook

├── README.md

├── LICENSE

└── .gitignore

---

## Analysis Coverage

### 1. Data Preparation
- Stratified sampling (5% per hour per date) across all 12 monthly files
- Combined into a single analysis-ready dataframe (~1.83M rows)

### 2. Data Cleaning
- Dropped non-analytical columns (store_and_fwd_flag)
- Resolved duplicate airport_fee columns
- Fixed negative monetary values
- Imputed missing values (median for numeric, mode for categorical)
- Removed outliers: invalid passenger counts, zero-fare anomalies, 
  extreme distances, invalid payment types

### 3. Exploratory Analysis

**Temporal**
- Busiest hour: 18:00 (estimated 2.58M actual trips)
- Peak window: 15:00–19:00 consistently across all months
- October and May are highest revenue months; February is weakest
- Q2 and Q4 together contribute 53.6% of annual revenue

**Financial**
- Trip distance vs fare correlation: 0.95 (strongest predictor)
- Trip duration vs fare correlation: 0.88
- Passenger count vs fare correlation: 0.04 (negligible)
- Trip distance vs tip amount correlation: 0.73
- Credit card dominates at 81.5% of all payments
- Night hours (11PM–5AM) generate 12.1% of revenue despite fewer hours

**Geographical**
- Top pickup zones: JFK Airport (96,755), Upper East Side South (86,895), 
  Midtown Center (85,930)
- JFK pickup/dropoff ratio: 4.63 — severe cab repositioning gap
- Newark Airport ratio: 0.04 — high dropoff accumulation, near-zero pickups

**Pricing**
- VeriFone charges ~80% more per mile than CMT on short trips 
  (≤2 miles: $17.93 vs $9.93)
- Rates converge on medium and long trips
- Fare per mile per passenger drops from $10.86 (solo) to $1.35 (6 passengers)
- Shorter, cheaper trips tip at higher percentages

---

## Key Recommendations

1. **Fleet deployment** — Concentrate availability between 15:00–19:00 
   in Midtown and Upper East Side zones
2. **Repositioning** — Incentivize drivers at high-dropoff zones 
   (Newark, Greenpoint) to move to high-pickup zones after each drop
3. **Pricing** — Surge pricing during peak hours; flat rates for airport 
   routes; shared-ride pricing for 3–6 passenger trips
4. **Vendor audit** — VeriFone's short-trip pricing is a competitive 
   liability and warrants review
5. **Night operations** — Increase Fri/Sat night fleet; night trips carry 
   high per-trip value despite lower volume

---

## How to Run

1. Clone this repository
2. Download the 2023 TLC trip records from the link above
3. Place parquet files in a `data/trip_records/` folder
4. Place taxi zone shapefile in `data/taxi_zones/`
5. Open `nyc_taxicab_eda.ipynb` in Jupyter or Google Colab
6. Update the file paths in the notebook to match your local folder structure
7. Run all cells


