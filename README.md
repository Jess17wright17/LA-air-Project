# LA Air Quality Monitoring Gap Analysis

A data tool that identifies which neighborhoods in Los Angeles County have the worst air quality, the highest poverty rates, and no nearby air quality sensors — and turns that into a deployment plan for low-cost monitors.

**[View the full report and interactive map](https://jess17wright17.github.io/LA-air-Project/la_air_quality_report.html)** · **[Government monitor placement map](https://jess17wright17.github.io/LA-air-Project/government_monitor_map.html)**

---

## The problem

PurpleAir is a citizen-run network of low-cost air quality sensors. Anyone can buy one and plug it in — but at $250 each, they cluster in wealthy neighborhoods. The result is that the communities with the worst air pollution have the least data about it.

This isn't just an observation. Peer-reviewed research from UC Irvine confirmed it directly:

- [Sun et al. (2022), *American Journal of Public Health*](https://pubmed.ncbi.nlm.nih.gov/35196049/) — Fewer PurpleAir sensors in California census tracts with lower income, higher PM2.5, and higher proportions of racial and ethnic minority populations
- [Mullen et al. (2022), *Environmental Research*](https://pubmed.ncbi.nlm.nih.gov/34953883/) — Tracts with higher percentages of Hispanic, Latino, and Black residents and lower median household income had significantly fewer sensors in LA County

Official EPA monitors have the same problem. There are roughly 35 regulatory monitors for all of LA County — a county of 10 million people — and their placement reflects decisions made decades ago, not current community need.

Better data leads to enforcement. Without it, communities have fewer tools to document violations, build legal cases, or hold polluters accountable.

---

## What this analysis does

The analysis pulls live sensor locations from the PurpleAir API and combines them with California's official CalEnviroScreen 4.0 dataset, which scores every census tract in the state on pollution burden and socioeconomic vulnerability.

It then:

- Fetches the locations of all outdoor PurpleAir sensors in LA County
- Loads CalEnviroScreen 4.0 data for all 2,305 LA County census tracts
- Calculates the distance from each tract to its nearest sensor
- Flags tracts in the top 30% for PM2.5 **and** top 40% for poverty **and** with no sensor within 1.5km as priority zones
- Ranks those priority zones by PM2.5 percentile to find the most urgent deployment targets

The result is 222 priority census tracts — real neighborhoods breathing documented bad air with no monitoring nearby.

---

## What's in this repository

- **README.md** — this file
- **la_air_quality_report.html** — the full report with the interactive map embedded
- **la_air_quality_gaps.html** — the standalone interactive map
- **government_monitor_map.html** — map of official EPA/regulatory monitor placement
- **priority_deployment_zones.csv** — the full list of all 222 priority tracts with coordinates and rankings

---

## How to use it

Start with the report. It explains the problem, walks through the methodology, lists the top 10 priority deployment zones, and embeds the interactive map. On the map, red dots are priority deployment zones, orange are lower-priority coverage gaps, green are adequately covered areas, and blue are existing PurpleAir sensors. Click any dot for details.

The coordinates in `priority_deployment_zones.csv` are census tract centroids — a starting point for finding a building, school, or community organization to host a sensor.

---

## Next steps

1. **Contact a community organization.** East Yard Communities for Environmental Justice (eastyard.org) and Communities for a Better Environment (cbecal.org) work in exactly these neighborhoods. Share this report and ask where they need sensors most.
2. **Build a prototype sensor.** A Raspberry Pi Zero W with a PMS5003 sensor and a weatherproof case costs about $50. Test it for two weeks next to an existing PurpleAir sensor to validate accuracy before deployment.
3. **Find host locations.** Schools, churches, community centers, and willing residents in priority tracts. The sensor needs power and WiFi — nothing else.
4. **Publish the data.** Feed readings into a public dashboard and make it embeddable so community organizations can put it on their own sites.

---

## Data sources

- PurpleAir API — real-time low-cost sensor locations and readings
- CalEnviroScreen 4.0 (OEHHA / CalEPA) — pollution burden and socioeconomic scores by census tract

Analysis by Jess Wright.
