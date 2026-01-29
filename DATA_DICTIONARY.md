# Data Dictionary

This document describes the structure and variables in the processed weather dataset.

## Dataset Overview

- **Source**: INMET (Instituto Nacional de Meteorologia)
- **Coverage**: São Paulo State, Brazil
- **Period**: 2000 - Present
- **Temporal Resolution**: Daily (aggregated from hourly data)
- **Number of Stations**: ~47 weather stations

## Data Structure

The processed data is stored in `Data.xlsx` with the following structure:

### Main DataFrame Columns

| Column Name | Data Type | Unit | Description |
|------------|-----------|------|-------------|
| `estacao` | string | - | Weather station name |
| `data` | datetime | - | Date of measurement |
| `regiao` | string | - | Region code (e.g., 'SE' for Southeast) |
| `uf` | string | - | State code (always 'SP' for São Paulo) |
| `codigo_wmo` | string | - | WMO (World Meteorological Organization) station code |
| `latitude` | float | degrees | Station latitude (-90 to 90) |
| `longitude` | float | degrees | Station longitude (-180 to 180) |
| `altitude` | float | meters | Station elevation above sea level |

### Meteorological Variables

#### Temperature Variables
| Column Name | Data Type | Unit | Description |
|------------|-----------|------|-------------|
| `temperatura_ar` | float | °C | Mean air temperature for the day |
| `temperatura_maxima` | float | °C | Maximum air temperature recorded |
| `temperatura_minima` | float | °C | Minimum air temperature recorded |
| `temperatura_orvalho` | float | °C | Mean dew point temperature |

#### Humidity Variables
| Column Name | Data Type | Unit | Description |
|------------|-----------|------|-------------|
| `umidade_relativa` | float | % | Mean relative humidity (0-100) |
| `umidade_relativa_maxima` | float | % | Maximum relative humidity |
| `umidade_relativa_minima` | float | % | Minimum relative humidity |

#### Precipitation Variables
| Column Name | Data Type | Unit | Description |
|------------|-----------|------|-------------|
| `precipitacao` | float | mm | Total daily precipitation (sum of hourly values) |

#### Pressure Variables
| Column Name | Data Type | Unit | Description |
|------------|-----------|------|-------------|
| `pressao_atmosferica` | float | hPa | Mean atmospheric pressure at station level |

#### Wind Variables
| Column Name | Data Type | Unit | Description |
|------------|-----------|------|-------------|
| `vento_velocidade` | float | m/s | Mean wind speed |
| `vento_direcao` | float | degrees | Mean wind direction (0-360, meteorological convention) |
| `vento_rajada` | float | m/s | Maximum wind gust speed |

#### Radiation Variables
| Column Name | Data Type | Unit | Description |
|------------|-----------|------|-------------|
| `radiacao_global` | float | KJ/m² | Total daily global solar radiation |

### Derived Indices

These indices are calculated in the ETL process:

| Column Name | Data Type | Unit | Description | Formula |
|------------|-----------|------|-------------|---------|
| `Heat Index` | float | °C | Apparent temperature combining air temp and humidity | Based on Steadman's formula |
| `WCI` | float | dimensionless | Wind Chill Index - perceived temperature due to wind | (10√V - V + 10.5)(33 - T) |
| `Humidex` | float | dimensionless | Canadian humidity index combining temp and dew point | T + 0.5555(e - 10) |

## Index Formulas

### Heat Index (HI)
```
HI = -8.78469475556 + 1.61139411*T + 2.33854883889*R 
     - 0.14611605*T*R - 0.012308094*T² - 0.0164248277778*R²
     + 0.002211732*T²*R + 0.00072546*T*R² - 0.000003582*T²*R²
```
Where:
- T = Air temperature (°C)
- R = Relative humidity (%)

### Wind Chill Index (WCI)
```
WCI = (10√V - V + 10.5)(33 - T)
```
Where:
- V = Wind speed (m/s)
- T = Air temperature (°C)

### Humidex
```
Humidex = T + 0.5555(e - 10)
e = 6.11 * exp(5417.7530 * (1/273.16 - 1/T_o_K))
```
Where:
- T = Air temperature (°C)
- T_o = Dew point temperature (°C)
- T_o_K = Dew point in Kelvin
- e = Vapor pressure (hPa)

## Weather Stations

### Example Stations in São Paulo State

| Station Name | City | Latitude | Longitude | Altitude (m) |
|--------------|------|----------|-----------|--------------|
| SAO PAULO - MIRANTE | São Paulo | -23.50 | -46.62 | 792 |
| SAO PAULO - INTERLAGOS | São Paulo | -23.75 | -46.70 | 805 |
| SOROCABA | Sorocaba | -23.50 | -47.45 | 601 |
| CAMPINAS | Campinas | -22.90 | -47.07 | 669 |
| SANTOS | Santos | -23.94 | -46.30 | 4 |

*Full list of 47 stations available in the dataset*

## Data Quality Notes

### Missing Values
- Represented as `NaN` or `null`
- Common in older data (2000-2005)
- More complete for recent years (2020+)

### Data Gaps
- Some stations have gaps due to:
  - Equipment maintenance
  - Technical failures
  - Station relocations
  - Late installation dates

### Aggregation Method
- **Temperature, Pressure, Humidity, Wind**: Mean (average) of hourly values
- **Precipitation**: Sum of hourly values
- **Max/Min values**: Maximum/minimum of hourly readings

### Data Filtering
- Only São Paulo state (UF='SP') data is included
- Empty rows (all weather variables null) are removed
- Dates and times are validated and converted

## Usage Examples

### Filter by City
```python
sorocaba_data = df[df['estacao'] == 'SOROCABA']
```

### Filter by Date Range
```python
recent_data = df[df['data'] >= '2020-01-01']
```

### Calculate Monthly Averages
```python
monthly = df.groupby([df['data'].dt.year, df['data'].dt.month])['temperatura_ar'].mean()
```

### Find Hottest Days
```python
hottest = df.nlargest(10, 'temperatura_maxima')
```

## References

1. INMET - Instituto Nacional de Meteorologia: https://portal.inmet.gov.br/
2. Heat Index formula: Steadman, R.G. (1979). Journal of Applied Meteorology
3. Humidex: Environment and Climate Change Canada
4. WMO Station codes: World Meteorological Organization

## Update History

- **2025-01**: Initial data dictionary created
- Data structure reflects ETL.ipynb processing as of January 2025

---

For questions about specific variables or data interpretation, please open an issue in the repository.
