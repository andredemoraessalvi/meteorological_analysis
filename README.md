# Weather Data Analysis - São Paulo State (INMET)

## 📋 Project Description

This project performs ETL (Extract, Transform, Load) and exploratory data analysis on meteorological data from the Brazilian National Institute of Meteorology (INMET) for weather stations in São Paulo state. It includes time series forecasting using LSTM neural networks.

## 🌟 Features

- **Data Extraction**: Automated download of historical weather data from INMET portal (2000-present)
- **Data Processing**: Cleaning, transformation, and aggregation of meteorological data
- **Custom Metrics**: Calculation of derived indices:
  - Heat Index (HI)
  - Wind Chill Index (WCI)
  - Humidex
- **Interactive Visualizations**: Heat maps and time series analysis
- **Machine Learning**: LSTM-based temperature prediction with 60-day forecasting
- **Interactive Widgets**: Dynamic city selection for analysis

## 📊 Dataset

The project uses historical meteorological data from INMET's BDMEP (Banco de Dados Meteorológicos para Ensino e Pesquisa), covering:
- **Period**: 2000 to present
- **Region**: São Paulo state, Brazil
- **Weather Stations**: 47 stations across the state
- **Variables**: Temperature, humidity, precipitation, wind speed, atmospheric pressure, and more

## 🛠️ Technologies Used

- **Python 3.10.9**
- **Data Processing**: pandas, numpy
- **Visualization**: matplotlib, folium (interactive maps)
- **Machine Learning**: TensorFlow/Keras (LSTM)
- **Web Requests**: httpx
- **Others**: tqdm, ipywidgets, scikit-learn

## 📁 Project Structure

```
.
├── ETL.ipynb              # Data extraction and processing notebook
├── DS.ipynb               # Data analysis and ML modeling notebook
├── requirements.txt       # Python dependencies
├── .gitignore            # Git ignore file
└── README.md             # This file
```

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or higher
- pip package manager

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd <repository-name>
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the ETL notebook to download and process data:
```bash
jupyter notebook ETL.ipynb
```

4. Run the analysis notebook:
```bash
jupyter notebook DS.ipynb
```

## 📓 Notebooks

### ETL.ipynb
- Downloads ZIP files from INMET portal for years 2000-2024
- Extracts and processes CSV files from ZIP archives
- Filters data for São Paulo state only
- Aggregates hourly data to daily averages/sums
- Calculates Heat Index, Wind Chill Index, and Humidex
- Exports processed data to `Data.xlsx`

### DS.ipynb
- Imports processed data from `Data.xlsx`
- Exploratory data analysis with interactive visualizations
- Time-animated heat map showing temperature distribution across SP state
- LSTM model for temperature prediction:
  - 80% training / 20% testing split
  - 30-day sliding window
  - 60-day future forecasting
  - Performance metrics: MAE, RMSE, R²

## 📈 Key Metrics

The project calculates the following derived metrics:

1. **Heat Index (HI)**: Apparent temperature combining air temperature and relative humidity
2. **Wind Chill Index (WCI)**: Perceived decrease in temperature due to wind
3. **Humidex**: Canadian-developed index combining temperature and dew point

## 🗺️ Interactive Features

- Time-animated heat map showing temperature evolution across São Paulo state
- Interactive city selector for LSTM predictions
- Customizable forecast periods

## 📊 Model Performance

The LSTM model provides temperature predictions with:
- Mean Absolute Error (MAE) typically < 2°C
- R² scores > 0.85 for most weather stations
- 60-day forecasting capability

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is open source and available under the MIT License.

## 📧 Contact

For questions or suggestions, please open an issue in the repository.

## 🙏 Acknowledgments

- INMET (Instituto Nacional de Meteorologia) for providing open meteorological data
- Original data collection methodology adapted from [dkko.me](https://dkko.me/posts/coleta-tratamento-inmet-bdmep/)

## ⚠️ Note

The local file paths in the notebooks (e.g., `C:/Users/z004wshk/...`) should be updated to match your environment before running the code.
