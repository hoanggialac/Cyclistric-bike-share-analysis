🚲 Cyclistic Bike Share Analysis
How do annual members and casual riders use Cyclistic bikes differently?

Portfolio Project | Business Analyst / Data Analyst
Tools: Python · SQL · Power BI / Tableau · Excel
Dataset: Divvy Trip Data — April 2024 (415K rides)


📌 Business Context
Cyclistic is a Chicago-based bike-share company with 5,800+ bicycles and 600+ docking stations. The marketing team believes that converting casual riders (single-ride or day-pass users) into annual members is key to long-term growth.
The core question:

What behavioural differences exist between casual riders and annual members — and how can these insights drive a targeted marketing strategy?


📁 Project Structure
cyclistic-analysis/
│
├── 📓 cyclistic_analysis.py      # Python EDA & visualizations
├── 🗄️  cyclistic_sql_analysis.sql # SQL business queries (10 questions)
├── 📊 cyclistic_charts.png        # Output charts
├── 📋 cyclistic_summary.csv       # Aggregated data (for Power BI / Tableau)
├── 🧹 cyclistic_clean.csv         # Cleaned dataset
└── 📝 README.md

🔍 Methodology
1. Data Collection

Source: Kaggle — Divvy Bike Sharing (April 2024)
Raw data: 415,025 ride records, 13 columns
Key fields: ride_id, rideable_type, started_at, ended_at, start/end station, lat/lng, member_casual

2. Data Cleaning (Python / pandas)
IssueActionRows AffectedNegative ride durationRemoved188 rowsDuration > 24 hoursRemoved (likely docking errors)517 rowsMissing station namesFlagged, kept (lat/lng still valid)~19% of rowsFinal clean dataset414,320 rows
3. Feature Engineering
pythonride_duration_min = (ended_at - started_at).total_seconds() / 60
hour              = started_at.dt.hour
day_of_week       = started_at.dt.day_name()
is_weekend        = day_of_week.isin(['Saturday', 'Sunday'])

📊 Key Findings
Finding 1 — Rider Split
Rider TypeRidesShareAnnual Member282,98368.3%Casual131,33731.7%
Finding 2 — Ride Duration
Rider TypeAvg DurationMedianCasual21.4 min11.9 minMember11.8 min8.3 min

💡 Casual riders average nearly 2× longer per ride — indicating leisure/recreational use rather than commuting.

Finding 3 — Day of Week Pattern

Members ride heavily Mon–Fri (commute pattern), with a dip on weekends
Casual riders peak on Saturday–Sunday (43% of casual rides are on weekends vs only 25% for members)

Finding 4 — Time of Day

Members: Clear twin peaks at 8AM and 5PM → classic commuter signature
Casual riders: Single ramp-up peaking at 2–5PM → leisure pattern

Finding 5 — Top Casual Stations (Marketing Hotspots)
StationCasual RidesCasual %Streeter Dr & Grand Ave3,31976%DuSable Lake Shore Dr & Monroe St2,48278%Michigan Ave & Oak St1,31956%

💡 Top casual stations are all in tourist/lakefront areas — not residential or office corridors.


💡 Business Recommendations
Rec 1 — Weekend Membership Campaign

43% of casual rides happen on weekends

Launch a targeted weekend campaign: offer a discounted first month of annual membership to casual riders who ride 3+ times in a month. Activate via push notification right before their Saturday ride.
Rec 2 — Afternoon In-App Nudge

Casual ride peak: 2–5PM

At 1:30PM on weekends, send a personalised cost comparison: "You've spent $X on day passes this month. An annual membership would have saved you $Y."
Rec 3 — Long-Ride Loyalty Program

Casual classic bike avg: 41 min/ride

Introduce a "Ride More, Pay Less" tier: after 5 rides exceeding 20 minutes, trigger a one-click membership upgrade offer at a 20% discount.
Rec 4 — Station-Level Physical Marketing

Top 3 casual stations are all tourist/leisure corridors

Install membership sign-up QR codes at Streeter Dr, DuSable Lake Shore Dr, and Michigan Ave docks. These stations have 70–80% casual rider rates — highest conversion potential.

🛠️ Tools Used
ToolPurposePython (pandas, matplotlib, seaborn)EDA, data cleaning, visualisationSQL (PostgreSQL-compatible)Business queries, aggregationsPower BI / TableauInteractive dashboardExcelExecutive summary, pivot tables

📈 Dashboard (Power BI / Tableau)
The interactive dashboard covers 4 views:

Overview — KPIs, rider split, total rides
Behaviour — Hourly & daily patterns by rider type
Geography — Station-level heatmap (casual vs member concentration)
Insights — Duration distribution, bike preference, conversion funnel

→ View Dashboard (link to be added)

🚀 How to Reproduce
bash# 1. Clone the repo
git clone https://github.com/hoanggialac/cyclistic-bike-share-analysis.git
cd cyclistic-bike-share-analysis

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn

# 3. Add raw data
# Download from Kaggle and place in root folder:
# 202404-divvy-tripdata.csv

# 4. Run analysis
python cyclistic_analysis.py

📚 Data Source

Dataset: Divvy 2024–2025 Bike Sharing Data via Kaggle
Original provider: Motivate International Inc. / Lyft Bikes and Scooters
License: Divvy Data License Agreement
Data has been anonymised — no personally identifiable information is included.
