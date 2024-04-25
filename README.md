---

# TransEcon: Transportation and Economic Analysis in NYC

TransEcon is designed to investigate the influence of transportation infrastructure on economic development in New York City. This repository contains datasets and query to study the correlations between transportation access and various economic indicators.

## Project Objective

The aim of this project is to address key questions about the socioeconomic impacts of transportation infrastructure in NYC:

- How does transportation access influence economic growth, property values, and business activity in NYC?
- Are the economic benefits of transportation infrastructure equitably distributed across different demographic groups?
- Does the development of transportation infrastructure correlate with changes in employment rates in surrounding areas?

## Data

This project utilizes a variety of datasets sourced from public and governmental organizations. Below is a summary of the key datasets used:

| Name                   | Source                                      | Data Type | Format           | Resolution     | Link                                                                     |
|------------------------|---------------------------------------------|-----------|------------------|----------------|--------------------------------------------------------------------------|
| New York Boundaries    | NYC Open Data                               | Vector    | Shapefile        | N/A            | [NYC Open Data - Borough Boundaries](https://example.com)                |
| Subway Lines           | Metropolitan Transportation Authority       | GTFS      | TXT              | N/A            | [MTA Developers](https://example.com)                                   |
| Bus Routes             | Metropolitan Transportation Authority       | GTFS      | TXT              | N/A            | [MTA Developers](https://example.com)                                   |
| Airports               | NYC Open Data                               | Vector    | Shapefile        | N/A            | [NYC Open Data - AIRPORT_POLYGON](https://data.cityofnewyork.us/City-Government/AIRPORT_POLYGON/6dic-zdhf/about_data)   |
| DEM                    | New York State GIS Resource                 | Raster    | TIF              |  1 arc-second        | [USGS](https://apps.nationalmap.gov/downloader/)                            |
| Land Use               | Esri Sentinel-2 Land Cover  | Raster    | TIF              | 10 m| [Sentinel-2 Land Cover](https://livingatlas.arcgis.com/landcoverexplorer/#mapCenter=-77.08371%2C26.38100%2C11&mode=step&timeExtent=2017%2C2023&year=2023)           |
| Zoning        | Department of Finance (DOF)                 | File Database Format | Shapefile  | N/A            | [NYC Open Data - Zoning  Data](https://data.cityofnewyork.us/City-Government/Zoning-GIS-Data-Shapefile/kdig-pewd) |
| Property Values        | Department of Finance (DOF)                 | File Database Format | MDB  | N/A            | [NYC Open Data - Property Valuation and Assessment Data](https://data.cityofnewyork.us/City-Government/Property-Valuation-and-Assessment-Data/yjxr-fw8i/about_data) |



## General Data Processing

- All spatial data was reprojected to EPS:2263
  
- Convert GTFS data:first import the GTFS stops.txt and shapes.txt files into ArcGIS. Convert stop coordinates to point shapefiles and transform route coordinates from shapes.txt into line shapefiles, using tools "XY Table to Point" and "Points to Line", respectively.
- Data was clipped to New York City



## Data Normalization

### Airport
- Imported into database, non-essential fields were dropped using the following queries in pgAdmin :

```
ALTER TABLE airport
  DROP COLUMN operatorty,
  DROP COLUMN emergency,
  DROP COLUMN addrfull,
  DROP COLUMN capacitype,
  DROP COLUMN addrcity,
  DROP COLUMN osm_id,
  DROP COLUMN source,
  DROP COLUMN building,
  DROP COLUMN emergencyh;
```

### Initial airport table:
![alt text](pic/airport.png)

### Final airport table:
![alt text](pic/airport1.png)


### Road
- Imported into database, non-essential fields were dropped using the following queries in pgAdmin :
  
```
ALTER TABLE ny_road
  DROP COLUMN datemodifi,
  DROP COLUMN nysstreeti,
-- Include all other columns
```

### Final road table:
![alt text](pic/road.png)


### Bus route

- Imported into database, non-essential fields were dropped using the following queries in pgAdmin :
```
ALTER TABLE bus_route

  DROP COLUMN shape_leng,
  DROP COLUMN shape_id;
```

### Initial bus route table:
![alt text](pic/bus_route.png)


### Final bus route table:
![alt text](pic/busroute1.png)

### Bus stops
- Imported into database, non-essential fields were dropped using the following queries in pgAdmin :

```
ALTER TABLE bus_stops
  DROP COLUMN shape_id,
  DROP COLUMN sequence,
  DROP COLUMN stop_id,
-- Include all other columns
```

### Initial bus stop table:
![alt text](pic/bus_stop.png)

### Final bus stops table:
![alt text](pic/bus_stop1.png)

### Subway route
- Imported into database, non-essential fields were dropped using the following queries in pgAdmin :
```
ALTER TABLE subway_route

  DROP COLUMN shape_id,
-- Include all other columns
```

### Initial Subway route table:
![alt text](pic/subway_route.png)

### Final Subway route table:
![alt text](pic/subway_route1.png)

### Subway stops (same steps above )

### Final Subway stops table:
![alt text](pic/subway_stop1.png)
