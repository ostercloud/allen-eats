# Restaurant List Keeper - Claude Instructions

## Overview
This project is a personal restaurant tracking system using Google Sheets as a backend and an interactive map (map.html) to display and filter restaurants.

## How to Add Restaurants from a New Source

### Option 1: Provide a URL
If the page is publicly accessible (not behind a paywall), provide the URL and ask:
```
Parse restaurants from this page and create a CSV: [URL]
```

### Option 2: Copy-Paste Content
For paywalled sites (NYT, Eater, etc.), copy the article text and paste it with:
```
Parse these restaurants into a CSV:
[paste content here]
```

## CSV Format
All CSVs should match this format for compatibility with the map:

```csv
name,address,cuisine,style,price,source,notes,lat,lng,visited,my_rating,google_rating
```

### Column Definitions
| Column | Required | Description |
|--------|----------|-------------|
| name | Yes | Restaurant name |
| address | Yes | Full address with city/state for geocoding |
| cuisine | No | Type of food (Indian, Italian, etc.) |
| style | No | Dining style: formal, casual, or fast |
| price | No | Price range: $, $$, $$$, or $$$$ |
| source | No | Where the recommendation came from |
| notes | No | Any additional info (rankings, highlights) |
| lat | No | Latitude (will be geocoded if missing) |
| lng | No | Longitude (will be geocoded if missing) |
| visited | No | "yes" if visited, blank otherwise |
| my_rating | No | Personal rating 1-5 |
| google_rating | No | Google Maps rating (manual entry) |

## Geocoding
- If lat/lng are missing, the map will geocode addresses automatically (slow on first load)
- For instant loading, run the geocoding script to pre-populate coordinates
- Addresses should include city and state for best accuracy

## Workflow for Adding New Lists

1. **Parse the content** - Extract restaurant names, addresses, cuisines, and any other available info
2. **Create CSV** - Save to `/Users/aoster/Restuarant list Keeper/[source]-restaurants.csv`
3. Ensure there are no duplicates from other lists, look at the existing spreadsheet references in the index.html.
3. **Geocode** (optional) - Run geocoding to add lat/lng for instant map loading
4. **Merge or replace** - User can import CSV into their Google Sheet

## Example Sources
- NYT 100 Best Restaurants
- Eater 38
- Infatuation reviews
- Michelin Guide
- Local food blogs

## File Structure
```
/Users/aoster/Restuarant list Keeper/
├── indext.html                          # Main map application
├── README.md                         # This file
├── example.csv                       # Example list with coordinates
├── geocode-restaurants.cjs           # Node script for batch geocoding
└── [other source]-restaurants.csv    # Additional lists
```

## Google Sheet
- Sheet ID: `1P1U_HMXQq2OCcyS9RheUDZH0fFcCa-Tc_mUh0JIAtlU`
- Must be published (File → Share → Publish to web) for map to read it

## Tips for Parsing
- Restaurant names are usually in bold or headers
- Look for neighborhood/location info near names
- Extract cuisine type from descriptions
- Note any rankings or awards
- If address isn't provided, use restaurant name + neighborhood + "New York, NY"
