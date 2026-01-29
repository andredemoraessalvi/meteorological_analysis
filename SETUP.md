# Setup and Usage Guide

## Table of Contents
1. [System Requirements](#system-requirements)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Running the Notebooks](#running-the-notebooks)
5. [Data Flow](#data-flow)
6. [Troubleshooting](#troubleshooting)

## System Requirements

- **Operating System**: Windows, macOS, or Linux
- **Python**: 3.10 or higher
- **RAM**: Minimum 8GB (16GB recommended for large datasets)
- **Storage**: At least 5GB free space for downloaded data
- **Internet**: Required for downloading data from INMET

## Installation

### Step 1: Install Python

Download and install Python from [python.org](https://www.python.org/downloads/)

Verify installation:
```bash
python --version
```

### Step 2: Clone the Repository

```bash
git clone <repository-url>
cd <repository-name>
```

### Step 3: Create Virtual Environment

**On Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**On macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 4: Install Dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### Step 5: Verify Installation

```bash
python -c "import pandas, numpy, tensorflow, folium; print('All packages installed successfully!')"
```

## Configuration

### Update File Paths

Before running the notebooks, you need to update the local file paths:

1. **In ETL.ipynb**, find and update line 82:
```python
# Change this:
destdirpath = Path('C:/Users/z004wshk/OneDrive - Siemens Energy/Documents/BI Project')

# To your desired path:
destdirpath = Path('/path/to/your/data/folder')
```

2. **In DS.ipynb**, find and update line 28:
```python
# Make sure this matches the path where Data.xlsx is saved
df = pd.read_excel('Data.xlsx', 'Database')
```

## Running the Notebooks

### Step 1: Start Jupyter Notebook

```bash
jupyter notebook
```

This will open Jupyter in your default web browser.

### Step 2: Run ETL.ipynb

1. Open `ETL.ipynb`
2. Run all cells in order (Cell → Run All)
3. This will:
   - Download weather data from INMET (2000-2024)
   - Process and clean the data
   - Calculate derived metrics
   - Save processed data to `Data.xlsx`

**Note**: Initial data download may take 30-60 minutes depending on your internet speed.

### Step 3: Run DS.ipynb

1. Open `DS.ipynb`
2. Run all cells in order
3. This will:
   - Load processed data
   - Generate interactive visualizations
   - Train LSTM models
   - Create forecasts

## Data Flow

```
INMET Portal
    ↓
Download ZIP files (ETL.ipynb)
    ↓
Extract CSV files
    ↓
Filter São Paulo data
    ↓
Clean and aggregate
    ↓
Calculate metrics (HI, WCI, Humidex)
    ↓
Save to Data.xlsx
    ↓
Load into DS.ipynb
    ↓
Analyze and visualize
    ↓
Train ML models
    ↓
Generate predictions
```

## Troubleshooting

### Issue: Import errors

**Solution**: Make sure all dependencies are installed
```bash
pip install -r requirements.txt --force-reinstall
```

### Issue: TensorFlow installation fails

**Solution**: Install specific version for your system
```bash
# For CPU only
pip install tensorflow-cpu==2.13.0

# For GPU (requires CUDA)
pip install tensorflow-gpu==2.13.0
```

### Issue: Jupyter kernel crashes

**Solution**: Increase memory or process data in smaller batches
- Modify the year range in ETL.ipynb to download fewer years at a time

### Issue: ZIP download fails

**Solution**: 
- Check your internet connection
- The INMET server may be temporarily down - try again later
- Download specific years manually from [INMET Portal](https://portal.inmet.gov.br/dadoshistoricos)

### Issue: Heat map doesn't display

**Solution**: Make sure you trust the notebook in Jupyter
- File → Trust Notebook

### Issue: Path errors on Windows

**Solution**: Use raw strings or forward slashes
```python
# Instead of:
path = 'C:\Users\name\folder'

# Use:
path = r'C:\Users\name\folder'  # raw string
# OR
path = 'C:/Users/name/folder'   # forward slashes
```

### Issue: Memory errors with large datasets

**Solution**: Process data in chunks
```python
# Add chunksize parameter
for chunk in pd.read_csv('file.csv', chunksize=10000):
    # process chunk
```

## Performance Tips

1. **Use SSD** for data storage to improve I/O speed
2. **Close other applications** when training ML models
3. **Use GPU** if available for TensorFlow (requires CUDA setup)
4. **Cache intermediate results** to avoid reprocessing
5. **Process subset of data** during development/testing

## Getting Help

If you encounter issues not covered here:
1. Check the [Issues](../../issues) page
2. Search for similar problems
3. Create a new issue with:
   - Error message
   - Steps to reproduce
   - Your environment details

## Next Steps

After successful setup:
1. Explore the data in `DS.ipynb`
2. Try different cities in the LSTM prediction widget
3. Modify parameters (window size, epochs) to improve predictions
4. Add your own analyses and visualizations

Happy analyzing! 📊
