# Economic Development and Transportation Infrastructure

To discover the impact of transportation infrastructure on economic development in New York City

Binghui li
4/19/2024

## Objectives

- How does transportation access influence economic growth, property values, and business activity in NYC?
- Are the economic benefits of transportation infrastructure equitably distributed across different demographic groups?
- Does the development of transportation infrastructure correlate with changes in employment rates in surrounding areas?

## General Data Processing

- All spatial data was reprojected to EPS:2263
  
- Convert GTFS data:first import the GTFS stops.txt and shapes.txt files into ArcGIS. Convert stop coordinates to point shapefiles and transform route coordinates from shapes.txt into line shapefiles, using tools "XY Table to Point" and "Points to Line", respectively.
- Data was clipped to New York City

### Data

| Name               | Source                                   | Data Type | Format | Resolution       | Link                                                                        |
|--------------------|------------------------------------------|-----------|--------|-------------------|-----------------------------------------------------------------------------|
| New York Boundaries| NYC Open Data                            | Vector    | Shapefile | N/A             | [NYC Open Data - Borough Boundaries](https://data.cityofnewyork.us/City-Government/Borough-Boundaries/tqmj-j8zm) |
| Subway Lines       | Metropolitan Transportation Authority    | GTFS      | TXT    | N/A               | [MTA Developers](https://new.mta.info/developers)                            |
| Bus Routes         | Metropolitan Transportation Authority    | GTFS      | TXT    | N/A               | [MTA Developers](https://new.mta.info/developers)                            |
| Airports           | OpenStreetMap                            | Vector    | Shapefile | N/A             | [Humanitarian Data Exchange - New York Airports](https://data.humdata.org/dataset/hotosm_usa_newyork_airports) |
| DEM                | New York State GIS Resource             | Raster    | TIF    | 1 Meter           | [NYS GIS Clearinghouse](https://gis.ny.gov/nys-dem)                          |
| Land Use           | Office of Technology and Innovation (OTI)| Raster    | TIF    | 6-In Resolution  | [NYC Open Data - Land Cover Raster Data](https://data.cityofnewyork.us/Environment/Land-Cover-Raster-Data-2017-6in-Resolution/he6d-2qns/about_data) |
| Property Values    | Department of Finance (DOF)             | File Database Format | MDB | N/A            | [NYC Open Data - Property Valuation and Assessment Data](https://data.cityofnewyork.us/City-Government/Property-Valuation-and-Assessment-Data/yjxr-fw8i/about_data) |
| Business Licenses  | Department of Small Business Services (SBS) | CSV    | N/A    | N/A               | [NYC Open Data - SBS Certified Business List](https://data.cityofnewyork.us/Business/SBS-Certified-Business-List/ci93-uc8s/about_data) |


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
