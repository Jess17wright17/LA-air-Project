LA Air Quality Monitoring Gap Analysis
A data tool that identifies which neighborhoods in Los Angeles County have the worst air quality, the highest poverty rates, and no nearby air quality sensors — and turns that into a deployment plan for low-cost monitors.
View the interactive map · View the full report · Government monitor placement map
---
The problem
PurpleAir is a citizen-run network of low-cost air quality sensors. Anyone can buy one and plug it in — but at $250 each, they cluster in wealthy neighborhoods. The result is that the communities with the worst air pollution have the least data about it.
This isn't just an observation. Peer-reviewed research from UC Irvine confirmed it directly:
Sun et al. (2022), American Journal of Public Health — Fewer PurpleAir sensors in California census tracts with lower income, higher PM2.5, and higher proportions of racial and ethnic minority populations
Mullen et al. (2022), Environmental Research — Tracts with higher percentages of Hispanic, Latino, and Black residents and lower median household income had significantly fewer sensors in LA County
Official EPA monitors have the same problem. There are roughly 35 regulatory monitors for all of LA County — a county of 10 million people — and their placement reflects decisions made decades ago, not current community need.
Better data leads to enforcement. Without it, communities have fewer tools to document violations, build legal cases, or hold polluters accountable.
---
What this tool does
Three Python scripts that together produce an actionable gap analysis:
`air_quality_gap_analysis.py`
Fetches live PurpleAir sensor locations via the PurpleAir API (841 sensors in LA County)
Loads 96 official EPA regulatory monitor locations from the EPA AQS database
Loads CalEnviroScreen 4.0 data for all 2,305 LA County census tracts
Calculates the distance from each tract to its nearest sensor (PurpleAir or EPA)
Flags tracts in the top 30% for PM2.5 pollution AND top 40% for poverty AND with no sensor within 1.5km as priority zones
Outputs an interactive map and ranked CSV of priority deployment targets
`generate_report.py`
Reads the analysis output and generates a shareable HTML report explaining the findings in plain English
`government_monitor_map.py`
Maps official government monitor locations against the pollution and poverty burden to visualize placement bias
`fetch_epa_monitors.py`
One-time download of EPA AQS regulatory monitor locations for LA County (no API key needed)
---
Findings
Running against current data (June 2026):
Metric	Value
PurpleAir sensors in LA County	838
EPA regulatory monitors in LA County	96
Total sensors combined	934
LA County census tracts analyzed	2,305
Priority deployment zones identified	222
222 census tracts in LA County currently have air quality in the worst 30% of the county, poverty rates in the worst 40%, and no air quality sensor — citizen or official — within 1.5km. These are concentrated in Watts, Wilmington, Compton, Boyle Heights, and East LA.
---
Data sources
Source	What it provides	Access
PurpleAir API	Live citizen sensor locations and readings	Free API key
CalEnviroScreen 4.0	PM2.5, poverty, and 19 other indicators for every CA census tract	Free download
EPA AQS Sites	Official regulatory monitor locations nationwide	Free, no key needed
---
Setup
Requirements
```
pip install requests pandas folium scipy openpyxl
```
PurpleAir API key
Sign up free at develop.purpleair.com. Set as environment variable:
```
# Windows
set PURPLEAIR_API_KEY=your_key_here

# Mac/Linux
export PURPLEAIR_API_KEY=your_key_here
```
CalEnviroScreen data
Download the Excel file from oehha.ca.gov/calenviroscreen/download-data and save as `calenviroscreen.xlsx` in the project folder.
---
Usage
```bash
# One time — download EPA monitor locations
python fetch_epa_monitors.py

# Run the analysis (generates map + CSV)
python air_quality_gap_analysis.py

# Generate the shareable report
python generate_report.py

# Generate the government monitor placement map
python government_monitor_map.py
```
Outputs:
`la_air_quality_gaps.html` — interactive map of all findings
`la_air_quality_report.html` — shareable report with methodology and findings
`government_monitor_map.html` — government monitor placement vs burden
`priority_deployment_zones.csv` — ranked list of 222 priority tracts with coordinates
---
What's next
The analysis is a deployment plan. The goal is to place low-cost air quality sensors in the 222 identified priority zones — starting with the highest ranked tracts in Watts, Wilmington, and Compton.
Hardware options:
PurpleAir PA-II (~$250) — plug and play, data goes public automatically
DIY Raspberry Pi Zero W + PMS5003 sensor (~$50) — for locations without WiFi
Organizations working in these communities:
East Yard Communities for Environmental Justice — Commerce/Southeast LA/Long Beach
Communities for a Better Environment — Huntington Park/Wilmington
Reference project:
The IVAN network in Imperial Valley is a working example of community air monitoring data leading to regulatory enforcement in California — by the same agency (SCAQMD) that covers LA.
---
Contributing
If you work in one of the identified neighborhoods and want to host a sensor, or if you're a developer who wants to contribute to the analysis, feel free to open an issue or get in touch.
---
License
MIT — use it, fork it, build on it.
---
Built by Jess Wright · Irvine, CA · 2026
Data refreshed June 2026
