# TeamInception Datathon - Time Series Forecasting

This repository contains the solution for the TECH-TRIATHLON Datathon by Team Inception, focusing on time series forecasting for processing time prediction and staffing optimization.

## Project Overview

The project addresses two main tasks:
1. **Task 1**: Processing Time Prediction - Predicting the time required to complete various administrative tasks
2. **Task 2**: Staffing Optimization - Optimizing staff allocation using time series forecasting techniques

## Repository Structure

```
├── README.md
├── main.py                                          # Main execution script
├── pyproject.toml                                   # Project dependencies
├── uv.lock                                          # Dependency lock file
├── .python-version                                  # Python version specification
├── .gitignore                                       # Git ignore rules
│
├── dataset/                                         # Training datasets
│   ├── bookings_train.csv                          # Booking records
│   ├── staffing_train.csv                          # Staffing data
│   └── tasks.csv                                    # Task definitions
│
├── test_dataset/                                    # Test datasets
│
├── notebooks/                                       # Analysis notebooks
│   ├── dataset_preparation_notebook.ipynb          # Data preparation
│   ├── task1_eda_and_data_preprocessing.ipynb      # Task 1 basic EDA
│   ├── task1_eda_and_data_preprocessing_LSTM.ipynb # Task 1 LSTM implementation
│   ├── task2_eda_and_data_preprocessing.ipynb      # Task 2 basic EDA
│   ├── task2_eda_and_data_preprocessing_LSTM.ipynb # Task 2 LSTM implementation
│   └── task2_eda_and_data_preprocessing_holtwintes.ipynb # Task 2 Holt-Winters
│
└── .ipynb_checkpoints/                              # Jupyter checkpoints
```

## Setup Instructions

### Prerequisites
- Python 3.8+
- UV package manager

### Installation

1. **Install UV package manager**
   
   Visit [installation | uv](https://docs.astral.sh/uv/getting-started/installation/) and follow the installation instructions for your operating system.

2. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd TeamInception_Datathon
   ```

3. **Install dependencies**
   ```bash
   uv sync
   ```
   This will create a virtual environment (.venv) and install all required dependencies.

4. **Activate the virtual environment** (if needed)
   ```bash
   source .venv/bin/activate  # On Linux/Mac
   # or
   .venv\Scripts\activate     # On Windows
   ```

### Running Notebooks

When running the Jupyter notebooks, make sure to select the kernel from the `.venv` virtual environment. If it's not automatically detected:

1. Open Jupyter/VS Code
2. Select the Python interpreter from `.venv/bin/python`
3. Run the notebooks in the following order:
   - `dataset_preparation_notebook.ipynb`
   - Task 1 notebooks: `task1_eda_and_data_preprocessing.ipynb` or `task1_eda_and_data_preprocessing_LSTM.ipynb`
   - Task 2 notebooks: Choose from the available preprocessing options

## Task Descriptions

### Task 1: Processing Time Prediction

**Objective**: Predict the processing time for administrative tasks based on historical booking data.

**Approach**:
- **Data Processing**: Clean and preprocess booking data, handle missing values
- **Feature Engineering**: Extract temporal features (year, month, day, weekday, hour, minute)
- **Model**: LSTM (Long Short-Term Memory) neural networks
- **Strategy**: Train separate models for each of the 19 task types for optimal performance

**Key Features**:
- 19 individual LSTM models (one per task type)
- Feature engineering from date/time components
- Comprehensive evaluation with MAE, RMSE, R², and accuracy metrics
- Visualization of actual vs predicted values and residual analysis

### Task 2: Staffing Optimization

**Objective**: Optimize staff allocation using time series forecasting techniques.

**Approaches**:
- **LSTM**: Deep learning approach for complex patterns
- **Holt-Winters**: Traditional statistical method for seasonal data
- **Comparative Analysis**: Evaluate different forecasting methods

## Technical Implementation

### Models Used

1. **LSTM Neural Networks**
   - Architecture: 64 LSTM units → Dropout (0.3) → Dense (32) → Dense (1)
   - Optimizer: Adam
   - Loss Function: Mean Absolute Error (MAE)
   - Training: 20 epochs with validation split

2. **Holt-Winters Exponential Smoothing**
   - Traditional time series forecasting
   - Handles seasonal patterns effectively

### Evaluation Metrics

- **MAE (Mean Absolute Error)**: Average absolute difference between predictions and actual values
- **RMSE (Root Mean Square Error)**: Square root of average squared differences
- **R² (Coefficient of Determination)**: Proportion of variance explained by the model
- **MAPE (Mean Absolute Percentage Error)**: Percentage-based error metric
- **Accuracy**: 100 - MAPE

## Data Description

### Datasets

1. **bookings_train.csv**: Historical booking records
   - appointment_date, appointment_time
   - task_id, citizen_id, booking_id
   - check_in_time, check_out_time
   - num_documents, queue_number, satisfaction_rating

2. **staffing_train.csv**: Staff allocation data
   - Staffing levels over time
   - Department/section information

3. **tasks.csv**: Task definitions and metadata
   - Task descriptions
   - Task categories

### Data Preprocessing

- Remove unnecessary columns (num_documents, queue_number, satisfaction_rating)
- Calculate actual processing time from check-in/check-out times
- Handle missing values appropriately
- Split data by task_id for individual model training
- Feature engineering for temporal patterns

## Results

The LSTM models achieve varying performance across different tasks:
- Task-specific optimization provides better accuracy than a single general model
- Performance metrics are tracked for each task individually
- Visual analysis through actual vs predicted plots and residual analysis

## Usage

### Running the Main Script
```bash
python main.py
```

### Running Individual Notebooks
Navigate to the specific notebook and run cells sequentially. Make sure to update file paths if running on different environments (e.g., local vs Google Colab).

### Google Colab Usage
Some notebooks are configured for Google Colab with Google Drive integration. Update the file paths in the data loading sections according to your Google Drive structure.

## Contributing

1. Follow the existing code structure
2. Update documentation for new features
3. Ensure all dependencies are added to pyproject.toml
4. Test changes across different environments

## Team

Team Inception - TECH-TRIATHLON Datathon Participants

## License

[Add appropriate license information]