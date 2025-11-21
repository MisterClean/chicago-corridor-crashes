# Wellington Avenue Corridor Crash Analysis

A comprehensive traffic crash analysis for the Wellington Avenue corridor in Chicago (Clybourn Avenue to Lake Shore Drive) supporting advocacy for the proposed **Wellington Greenway** cycling infrastructure.

**[View Live Report](https://misterclean.github.io/chicago-corridor-crashes/)**

## Overview

This project analyzes traffic crash data from 2019-2024 along the Wellington Avenue corridor to demonstrate the safety need for CDOT's proposed neighborhood greenway. The analysis provides data-driven evidence highlighting risks to vulnerable road users (cyclists and pedestrians) and emphasizes the importance of family-friendly infrastructure by examining crashes involving children.

**Created by:** [Lakeview Urbanists](https://lakeviewurbanists.org/)

## Background

The Chicago Department of Transportation (CDOT) has proposed the **Wellington Greenway**, a neighborhood greenway project that would improve safety along Wellington Avenue with features including:

- Advisory bike lanes
- Contraflow bike lanes
- 20 mph speed limit zones
- Traffic calming measures

This analysis supports this proposal by providing comprehensive crash statistics, identifying high-injury locations, and demonstrating the need for improved infrastructure to protect vulnerable road users.

## Data Sources

This analysis uses publicly available data from the City of Chicago:

1. **Traffic Crashes Dataset**
   - Source: [Chicago Data Portal - Traffic Crashes - Crashes](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if)
   - Timeframe: 2019-2024
   - Size: ~336MB
   - Contains crash-level data including location, date/time, injuries, contributing causes

2. **Traffic Crashes - People Dataset**
   - Source: [Chicago Data Portal - Traffic Crashes - People](https://data.cityofchicago.org/Transportation/Traffic-Crashes-People/u6pd-qa9d)
   - Size: ~463MB
   - Contains person-level demographic data for crash analysis

3. **Street Network Data**
   - Source: OpenStreetMap (queried automatically via osmdata package)
   - Used to define Wellington Avenue corridor and 150-foot buffer zone

## Requirements

### Software

- **R** (version 4.0 or higher recommended)
- **RStudio** (recommended for R Markdown)
- Internet connection (for OpenStreetMap queries)

### R Packages

```r
install.packages(c(
  "dplyr",           # Data manipulation
  "readr",           # CSV reading
  "sf",              # Spatial features
  "osmdata",         # OpenStreetMap data
  "lubridate",       # Date/time handling
  "stringr",         # String operations
  "tidyr",           # Data tidying
  "ggplot2",         # Visualization
  "leaflet",         # Interactive maps
  "leaflet.extras",  # Additional map features
  "knitr",           # Report generation
  "kableExtra",      # Enhanced tables
  "htmlwidgets",     # Interactive widgets
  "purrr",           # Functional programming
  "geosphere",       # Geographic calculations
  "ggmap",           # Mapping utilities
  "magrittr"         # Pipe operators
))
```

### System Requirements

- Minimum 8GB RAM recommended (for processing large CSV files)
- ~1GB free disk space for data files

## Installation & Setup

1. **Clone the repository**

```bash
git clone https://github.com/MisterClean/chicago-corridor-crashes.git
cd chicago-corridor-crashes
```

2. **Install R packages**

Open R or RStudio and run the installation command above.

3. **Download data files**

Due to their large size (~800MB total), the crash data CSV files are not included in the repository. Download them manually:

- Download [Traffic Crashes - Crashes](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if) as CSV
  - Save as `data/raw/crashes/traffic_crashes.csv`

- Download [Traffic Crashes - People](https://data.cityofchicago.org/Transportation/Traffic-Crashes-People/u6pd-qa9d) as CSV
  - Save as `data/raw/people/people.csv`

4. **Create data directories if needed**

```bash
mkdir -p data/raw/crashes
mkdir -p data/raw/people
```

## Usage

### Running the Analysis

1. Open `wellington_ave.Rmd` in RStudio

2. Click **Knit** to generate the HTML report, or run:

```r
rmarkdown::render("wellington_ave.Rmd")
```

3. The analysis will:
   - Load crash data from CSV files
   - Query OpenStreetMap for Wellington Avenue geometry
   - Create a 150-foot buffer zone around the corridor
   - Spatially join crashes within the buffer
   - Generate interactive maps and visualizations
   - Produce a self-contained HTML report

4. Output files:
   - `wellington_ave.html` - Main report
   - `docs/wellington_crashes.html` - GitHub Pages output

**Estimated run time:** 2-5 minutes (depending on system specs)

### Viewing the Report

Open `wellington_ave.html` in any web browser to view the interactive report with embedded maps and visualizations.

## Project Structure

```
chicago-corridor-crashes/
├── README.md                      # This file
├── wellington_ave.Rmd             # Main R Markdown analysis script
├── index.html                     # GitHub Pages deployment
├── R/
│   └── utils.R                    # Reusable utility functions
├── data/
│   └── raw/
│       ├── crashes/
│       │   └── traffic_crashes.csv    # Chicago crash data (not in repo)
│       └── people/
│           └── people.csv             # Person-level crash data (not in repo)
└── docs/
    └── wellington_crashes.html    # Generated report output
```

### Key Files

- **wellington_ave.Rmd** - Main analysis script (1046 lines) containing all data processing, spatial analysis, and visualization code
- **R/utils.R** - Shared utility functions for loading data, creating maps, calculating statistics, and generating summaries
- **.gitignore** - Excludes large CSV files and R artifacts from version control

## Analysis Features

The report includes the following sections:

### 1. Study Area Visualization
- Interactive map showing Wellington Avenue corridor with 150-foot buffer zone
- Spatial context for the analysis area

### 2. Demographics Analysis
- Age distribution of people involved in crashes
- Analysis of children involvement (under 18)
- Breakdown by person type (pedestrian, cyclist, driver, passenger)

### 3. Temporal Patterns
- Hourly distribution of crashes
- School hours analysis (7-9 AM and 2-4 PM)
- Day of week patterns

### 4. Seasonal Analysis
- Crash distribution across seasons
- Seasonal injury severity breakdown
- Vulnerable user trends by season

### 5. Safety Statistics
- Total crashes, injuries, and fatalities (2019-2024)
- Cyclist crash statistics
- Pedestrian crash statistics
- Children involvement statistics
- Hit-and-run incidents
- Dooring incidents

### 6. Interactive Maps
- **High Injury Locations** - Crash hotspots sized by injury severity
- **Cyclist Crashes** - All bicycle crashes with dooring incident flags
- **Pedestrian Crashes** - All pedestrian crashes along the corridor
- **Hexagonal Heat Map** - Spatial clustering visualization

### 7. Data Tables
- Detailed crash summaries
- Vulnerable road users statistics
- Seasonal breakdowns with monthly averages

## Outputs

### HTML Report

The analysis generates a **self-contained HTML report** (~2MB) that includes:

- Interactive Leaflet maps (zoom, pan, click for details)
- Embedded visualizations (charts, graphs, tables)
- Formatted narrative and statistics
- No external dependencies (works offline)

### GitHub Pages Deployment

The report is published to GitHub Pages for public access:
- **Live URL:** https://misterclean.github.io/chicago-corridor-crashes/

To update the published report:
1. Run the analysis to generate updated HTML
2. Copy output to `index.html`
3. Commit and push to GitHub

```bash
cp wellington_ave.html index.html
git add index.html
git commit -m "Update analysis report"
git push
```

## Methodology

### Spatial Analysis

1. **Corridor Definition**: Wellington Avenue geometry retrieved from OpenStreetMap
2. **Buffer Zone**: 150-foot buffer created around the street centerline using EPSG:3857 projection for accurate distance calculations
3. **Crash Selection**: Crashes spatially joined to buffer zone using coordinate-based filtering
4. **Temporal Filtering**: Data limited to 2019-2024 for current relevance

### Economic Impact

Crash costs estimated using National Safety Council (NSC) methodology:
- Fatal crashes: $1.7M per incident
- Incapacitating injuries: $155K per incident
- Non-incapacitating injuries: $32K per incident

### Visualization

- **Interactive maps** use Leaflet.js with custom styling
- **Statistical charts** created with ggplot2
- **Tables** formatted with kableExtra for professional presentation

## Contributing

We welcome contributions! If you'd like to:

- Report issues or suggest improvements: [Open an issue](https://github.com/MisterClean/chicago-corridor-crashes/issues)
- Contribute code or analysis: Fork the repository and submit a pull request
- Use this analysis for other corridors: Feel free to adapt the code (see License below)

## Future Enhancements

Potential additions to the analysis:

- Comparison with other Chicago corridors
- Before/after analysis if greenway is implemented
- Weather and lighting condition analysis
- Primary crash cause analysis
- Speed-related crash analysis
- Intersection-specific analysis

## Credits & Acknowledgments

- **Analysis & Development:** [Lakeview Urbanists](https://lakeviewurbanists.org/)
- **Data Source:** City of Chicago Data Portal
- **Street Network Data:** OpenStreetMap contributors
- **Tools:** R Statistical Software, RStudio, Leaflet.js

## License

This project is available under the MIT License. Feel free to use, modify, and distribute this analysis with attribution.

The data used in this analysis is provided by the City of Chicago under their [data portal terms of use](https://www.chicago.gov/city/en/narr/foia/data_disclaimer.html).

---

## Support the Wellington Greenway

If this analysis demonstrates the need for safer streets in your neighborhood, consider:

- Attending community meetings about the Wellington Greenway
- Contacting your alderperson to express support
- Joining [Lakeview Urbanists](https://lakeviewurbanists.org/) for local advocacy
- Sharing this analysis to raise awareness

**Safer streets save lives. Let's make Wellington Avenue safe for everyone.**
