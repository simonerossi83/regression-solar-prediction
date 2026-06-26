# regression-food-waste

## Project Overview
This project aims to develop a regression model to predict food waste generation (kg per capita per year) based on socioeconomic and demographic factors. The primary goal is to support decision-making and targeted interventions to reduce global food waste, aligning with UN Sustainable Development Goal 12.3.

## Research Question
Can we accurately predict food waste generation using socioeconomic and demographic factors (such as GDP per capita) to support strategies that promote sustainable consumption?

## Key Features
- **Data Integration**: Merges the Global Food Wastage Dataset (Kaggle) with World Bank GDP data.
- **Analysis**: Investigates the correlation between income levels and food waste.
- **Modeling**: Regression analysis to estimate waste based on Country, Year, Food Category, and GDP.

## Dependencies
To run the notebooks and scripts in this repository, you will need:
- Python 3.8+
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/food-waste-reduction.git
   ```
2. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```

## How to Run
1. **Data Acquisition**: Ensure you have the `Global Food Wastage Dataset` and the World Bank WDI dataset available in your project directory.
2. **Run Notebooks**: Open the main Jupyter/Colab notebook to execute the cells for Data Cleaning, EDA, and Model Training.
3. **Visualization**: Review the generated plots in the EDA section to understand the relationships between variables.

## Data Sources
- **Global Food Wastage Dataset (2018–2024)**: [Kaggle](https://www.kaggle.com/datasets/atharvasoundankar/global-food-wastage-dataset-2018-2024)
- **World Development Indicators**: [World Bank](https://databank.worldbank.org/source/world-development-indicators)

## License
This project uses data from the World Bank under the CC BY 4.0 license. Please refer to the specific license terms of the Kaggle dataset before redistribution.
