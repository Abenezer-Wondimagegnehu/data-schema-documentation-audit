# Database vs Documentation Gap Analysis

This analysis reviews the alignment between the production database schema and its corresponding documentation for the Berlin source data. It identifies gaps in table coverage, column mappings, data types, constraints, and provides recommendations for improvements. The analysis is based on a detailed column-by-column comparison in the attached spreadsheet (`final_Documentation.xlsx`).

🔗 [View Spreadsheet: final_Documentation](https://docs.google.com/spreadsheets/d/1sKv6KyHt4UwgK85ud2Lsxf01Bdv0AiiU1brqYr1V4jc/edit?usp=sharing)

## 1. Table Coverage Analysis

### 1.1 Common Tables (Present in Both Database and Documentation)

The following 27 tables exist in both the database and documentation, though with varying degrees of alignment in columns, data types, and constraints:

- banks
- dental_offices
- districts
- exhibition_centers
- galleries
- kindergartens
- long_term_listings
- milieuschutz_protection_zones
- museums
- neighborhoods
- parks
- playgrounds
- pharmacies
- pools
- public_artworks
- schools
- short_term_listings
- ubahn
- universities
- venues
- social_clubs_activities
- post_offices
- government_offices
- libraries
- religious_institutions
- petstores
- hospitals

### 1.2 Tables Only in Database (Missing from Documentation)

These 13 tables exist in the database but lack any documentation:

- bus_stops
- spas (corrected from spaetis for clarity)
- food_markets
- supermarkets
- tram_stops
- gyms
- doctors
- night_clubs
- sbahn
- recycling_points
- malls
- bike_lanes

> **Note**: Tables like `bus_stops` and `tram_stops` may have evolved from the documented `bus_tram_stops`. `dental_offices` exists in the DB and is partially documented (marked "In Progress").

### 1.3 Tables Only in Documentation (Missing from Database)

These 7 tables are documented but do not exist in the current database schema:

- bus_tram_stops
- districts_pop_stat
- regional_statistics
- vet_clinics
- crime_statistics
- land_prices
- rent_stats_per_neighborhood

> **Note**: `bus_tram_stops` appears to have been split into separate `bus_stops` and `tram_stops` tables in the database.

### Summary of Table Coverage

| Category                   | Count | Percentage of Total DB Tables |
|----------------------------|-------|-------------------------------|
| Common Tables              | 27    | 67.5%                         |
| Only in Database           | 13    | 32.5%                         |
| Only in Documentation      | 7     | -                             |
| **Total Database Tables**  | **40**| 100%                          |
| **Total Documented Tables**| **34**| -                             |

## 2. Detailed Gap Metrics

Based on the spreadsheet analysis, here is a summary of mismatches per table (for common tables). Mismatches include "Mismatch", "Partial", "Gap", etc.:

| Table Name                    | Name Mismatches | Data Type Mismatches | Constraint Mismatches | Undocumented Columns |
|-------------------------------|-----------------|----------------------|-----------------------|----------------------|
| banks                         | 6               | 18                   | 5                     | 2                    |
| dental_offices                | 9               | 21                   | 7                     | 3                    |
| districts                     | 1               | 2                    | 1                     | 1                    |
| exhibition_centers            | 4               | 15                   | 3                     | 3                    |
| galleries                     | 3               | 16                   | 3                     | 3                    |
| kindergartens                 | 8               | 16                   | 7                     | 4                    |
| long_term_listings            | 5               | 6                    | 3                     | 2                    |
| milieuschutz_protection_zones | 6               | 10                   | 4                     | 4                    |
| museums                       | 3               | 22                   | 3                     | 3                    |
| neighborhoods                 | 0               | 0                    | 0                     | 0                    |
| parks                         | 0               | 2                    | 0                     | 0                    |
| playgrounds                   | 0               | 2                    | 0                     | 0                    |
| pharmacies                    | 4               | 18                   | 2                     | 2                    |
| pools                         | 4               | 10                   | 3                     | 3                    |
| public_artworks               | 3               | 18                   | 3                     | 3                    |
| schools                       | 4               | 4                    | 3                     | 3                    |
| short_term_listings           | 3               | 4                    | 3                     | 3                    |
| ubahn                         | 4               | 9                    | 3                     | 3                    |
| universities                  | 4               | 10                   | 2                     | 2                    |
| venues                        | 4               | 20                   | 3                     | 3                    |
| social_clubs_activities       | 1               | 19                   | 0                     | 0                    |
| post_offices                  | 4               | 16                   | 3                     | 3                    |
| government_offices            | 2               | 16                   | 9                     | 0                    |
| libraries                     | 4               | 1                    | 0                     | 0                    |
| religious_institutions        | 4               | 26                   | 2                     | 2                    |
| petstores                     | 0               | 0                    | 0                     | 0                    |
| hospitals                     | 10              | 8                    | 8                     | 4                    |

## 3. Evaluation of Documentation Quality

- **Table-Level Descriptions**: All documented tables have basic descriptions, but some lack depth (e.g., business context or usage notes).
- **Column-Level Documentation**: Comprehensive for most, but undocumented columns are common (see Section 4).
- **Data Types and Constraints**: Frequent partial matches (e.g., "varchar" vs. "varchar(255)"), indicating incomplete specificity.
- **Overall Completeness**: 67.5% of DB tables are documented, but quality varies—many have high mismatch rates in data types.

## 4. Proposed Definitions for Undocumented Columns

Based on inferred usage from database structure and common patterns:

| Table Name                        | Column                   | Proposed Description                                                                 |
|-----------------------------------|--------------------------|--------------------------------------------------------------------------------------|
| banks                             | geometry                 | Spatial data object (Point) representing the bank's geographic location.             |
| banks                             | neighborhood             | Name or ID of the neighborhood where the bank is located.                            |
| dental_offices                    | geometry                 | Spatial data object for the dental office's location.                                |
| dental_offices                    | district                 | Administrative district of the dental office.                                        |
| dental_offices                    | neighborhood             | Specific neighborhood of the office.                                                 |
| districts                         | neighborhood             | List or reference to neighborhoods within the district.                              |
| exhibition_centers                | geometry                 | Spatial coordinates (Point or Polygon) for the center.                               |
| exhibition_centers                | district                 | Administrative district containing the center.                                       |
| exhibition_centers                | neighborhood             | Local neighborhood of the facility.                                                  |
| galleries                         | geometry                 | Geographic coordinates for the gallery.                                              |
| galleries                         | district                 | District designation for the gallery.                                                |
| galleries                         | neighborhood             | Neighborhood where the gallery operates.                                             |
| kindergartens                     | full_address             | Complete street address including postal code.                                       |
| kindergartens                     | geometry                 | Spatial location of the kindergarten.                                                |
| kindergartens                     | neighborhood_id          | Unique ID linking to a neighborhood record.                                          |
| kindergartens                     | postal_code              | Postal code for the kindergarten's location (added based on gap).                    |
| long_term_listings                | name                     | Title or descriptive name of the listing.                                            |
| long_term_listings                | neighborhood_id          | Unique ID for the listing's neighborhood.                                            |
| milieuschutz_protection_zones     | latitude                 | North-south coordinate of a central point in the zone.                               |
| milieuschutz_protection_zones     | longitude                | East-west coordinate of a central point in the zone.                                 |
| milieuschutz_protection_zones     | neighborhood             | Name of the neighborhood under protection.                                           |
| milieuschutz_protection_zones     | neighborhood_id          | Unique ID for the protected neighborhood.                                            |
| museums                           | district                 | Administrative district of the museum.                                               |
| museums                           | geometry                 | Spatial object for the museum's location.                                            |
| museums                           | neighborhood             | Local neighborhood of the museum.                                                    |
| pharmacies                        | geometry                 | Spatial coordinates for the pharmacy.                                                |
| pharmacies                        | neighborhood_id          | Unique ID linking to neighborhood.                                                   |
| pools                             | geometry                 | Spatial location of the pool facility.                                               |
| pools                             | neighborhood             | Neighborhood name for the pool.                                                      |
| pools                             | neighborhood_id          | Unique ID for the neighborhood.                                                      |
| public_artworks                   | district                 | Administrative district of the artwork.                                              |
| public_artworks                   | geometry                 | Spatial coordinates of the artwork.                                                  |
| public_artworks                   | neighborhood             | Local neighborhood of the artwork.                                                   |
| schools                           | geometry                 | Spatial data for the school campus.                                                  |
| schools                           | neighborhood             | Neighborhood associated with the school.                                             |
| schools                           | neighborhood_id          | Unique ID for the neighborhood.                                                      |
| short_term_listings               | name                     | Title or name of the listing.                                                        |
| short_term_listings               | neighborhood_id          | Unique ID for the neighborhood.                                                      |
| short_term_listings               | geometry                 | Spatial coordinates for the property.                                                |
| ubahn                             | name                     | Name of the U-Bahn station.                                                          |
| ubahn                             | geometry                 | Spatial location of the station.                                                     |
| ubahn                             | neighborhood_id          | Unique ID for the served neighborhood.                                               |
| universities                      | geometry                 | Spatial coordinates for the campus.                                                  |
| universities                      | neighborhood_id          | Unique ID for the neighborhood.                                                      |
| venues                            | geometry                 | Spatial coordinates for the venue.                                                   |
| venues                            | neighborhood_id          | Unique ID for the neighborhood.                                                      |
| venues                            | operating_hours_category | Classification of the venue's operating schedule.                                    |
| post_offices                      | district                 | Administrative district for the branch.                                              |
| post_offices                      | geometry                 | Spatial location of the post office.                                                 |
| post_offices                      | neighborhood             | Neighborhood of the branch.                                                          |
| religious_institutions            | district                 | Administrative district for the institution.                                         |
| religious_institutions            | neighborhood             | Neighborhood where the institution is located.                                       |
| hospitals                         | id                       | Unique identifier for the hospital (primary key).                                    |
| hospitals                         | geometry                 | Spatial location of the hospital.                                                    |
| hospitals                         | speciality               | Medical specialties offered by the hospital.                                         |
| hospitals                         | emergency                | Indicator if the hospital has emergency services.                                    |

## 5. Current Documentation Status Classification

**Complete and Accurate (0 Mismatches, 0 Undocumented)**:
- neighborhoods
- petstores

**Mostly Complete (Low Mismatches, 0 Undocumented)**:
- parks
- playgrounds
- social_clubs_activities
- government_offices
- libraries

**Incomplete (High Mismatches or Undocumented Columns)**:
- banks
- dental_offices
- districts
- exhibition_centers
- galleries
- kindergartens
- long_term_listings
- milieuschutz_protection_zones
- museums
- pharmacies
- pools
- public_artworks
- schools
- short_term_listings
- ubahn
- universities
- venues
- post_offices
- religious_institutions
- hospitals

### Key Observations
- **Primary Key Issues**: Missing in documentation for tables like `kindergartens`; `neighborhoods` has nullable ID.
- **Inconsistencies**: Varying formats for common fields (e.g., `opening_hours`, `wheelchair`, `phone`).
- **Data Type Gaps**: Frequent "Partial" matches due to unspecified lengths (e.g., varchar vs. varchar(255)).
- **Spatial Data**: Geometry columns are often undocumented across location-based tables.

## 6. Proposed Improvements

### Table Name Recommendations
| Current Name              | Recommended Name              | Rationale                            |
|---------------------------|-------------------------------|--------------------------------------|
| long_term_listings        | long_term_rental_listings     | Enhances clarity and specificity.    |
| short_term_listings       | short_term_rental_listings    | Enhances clarity and specificity.    |
| playgrounds                | public_playgrounds            | Reduces ambiguity.                   |
| ubahn                     | ubahn_subway_stations         | Improves international comprehension.|

### Technical and Documentation Recommendations
- **Standardize Data Types**: Use consistent specifications (e.g., always include length for varchar).
- **Add Constraints**: Document all PRIMARY/FOREIGN KEY and UNIQUE constraints explicitly.
- **Incorporate Spatial Data**: Add descriptions for `geometry`, `latitude`, `longitude` in all relevant tables.
- **Boolean Conversion**: Change fields like `short_term_listings.is_shared` from int2 to boolean.
- **Expand Descriptions**: Include usage examples, data sources, and update timestamps.
- **Automation**: Implement a script to generate documentation from DB schema for ongoing sync.

For full details, refer to the attached spreadsheet.