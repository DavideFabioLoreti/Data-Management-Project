# Impact of Weather Conditions on Air Quality: Integrated Analysis

This project explores the relationship between meteorological conditions and air quality across 21 European capitals by integrating data from weather and air pollution APIs. The system collects, validates, stores, and analyzes data to identify patterns and correlations useful for scientific, environmental, and public health applications.

## 📌 Project Overview

- **University**: University of Milano - Bicocca  
- **Course**: Master's Degree in Data Science  
- **Department**: DISCo – Department of Informatics, Systems and Communication  
- **Authors**: Davide Fabio Loreti (865309), Carlo Pegoraro (865329)

## 📡 Data Sources

- [WeatherAPI](https://www.weatherapi.com/) – Meteorological data
- [IQAir AirVisual](https://www.iqair.com/) – Air quality data  
- APIs used:
  - [WeatherAPI Docs](https://www.weatherapi.com/docs/)
  - [IQAir API Docs](https://api-docs.iqair.com/?version=latest)

## 🧱 Architecture

- **Data Collection**: Daily acquisition script using public APIs
- **Storage**: MongoDB (NoSQL)
- **Data Format**: JSON (hierarchical structure: `date → city → details`)
- **Data Quality**: Automatic validation of completeness, consistency, and value ranges
- **Enrichment**: Categorization of AQI values based on EPA standards

## 🔎 Key Queries (in Python)

- **Query 1**: Retrieve AQI for a specific city and date
- **Query 2**: Correlation between temperature and AQI
- **Query 3**: Top 5 windiest cities with respective AQI
- **Query 4**: Cities with the worst air quality on a specific day

## 🧠 Insights

- AQI levels can vary significantly based on weather conditions
- Wind speed plays a key role in pollutant dispersion
- Semantic enrichment (e.g., "Good", "Hazardous") improves data interpretability

## ⚙️ Technologies Used

- Python (data acquisition, validation, queries)
- MongoDB (data storage)
- APIs (WeatherAPI, IQAir)
- JSON (data exchange format)

## 🚀 Future Developments

- **Expand coverage** to additional cities and regions
- **Integrate new data sources** (e.g., traffic, IoT sensors, satellite data)
- **Implement predictive models** using machine learning
- **Perform advanced analytics** (e.g., spatiotemporal clustering, anomaly detection)

## 🌍 Practical Applications

- Public health monitoring
- Urban environmental planning
- Scientific research and climate studies

## 📑 License

This project is developed for academic purposes and is shared under the MIT License.

---
