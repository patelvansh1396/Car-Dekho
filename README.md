# Used Car Price Analysis (India)

Cleaning, merging and visualising four used-car listing datasets using only **Python, pandas, numpy and matplotlib**.

## 1. Project Definition
Used-car prices in India depend on many factors: age, kilometres driven, brand, fuel type and transmission. The raw data for this is scattered across four CSV files with different column names, units (lakhs vs rupees) and owner formats. This project **cleans and merges them into one consistent dataset**, then uses five visualizations to show what drives the resale price of a used car.

## 2. Dataset Use Case
| File | Rows | Notes |
|---|---|---|
| `car_data.csv` | 301 | Price in **lakhs**, owner as 0/1/3 |
| `CAR_DETAILS_FROM_CAR_DEKHO.csv` | 4,340 | Basic listing details |
| `Car_details_v3.csv` | 8,128 | Adds mileage, engine, power, seats |
| `car_details_v4.csv` | 2,059 | Adds location, colour, dimensions |

The cleaned dataset (`data/cleaned/cleaned_cars.csv`, 12,691 rows) can be used for:
- **Buyers/sellers**: judging whether a listing price is fair.
- **Dealers**: seeing which brands and fuel types sell most and at what price.
- **Machine learning** (future work): a price-prediction model.
- **Market analysis**: depreciation, transmission and fuel trends.

## 3. Data Cleaning (`cleaning_log.txt`)
1. Renamed columns to one schema: `brand, name, year, price_inr, km_driven, fuel, seller_type, transmission, owner, source`.
2. Converted `car_data.csv` prices from lakhs to rupees; mapped numeric owner codes to First/Second/Third/Fourth & Above.
3. Standardised text (strip spaces, consistent case); merged `Trustmark Dealer`/`Corporate` into `Dealer`; extracted brand from the car name.
4. Removed: test-drive/unregistered/unknown-owner rows (44), rare fuel types (6), impossible years (7), price < Rs 20,000 or km <= 0 (6), **duplicate listings (2,021)**, and extreme outliers by the IQR rule (53).
5. Added `car_age` and `price_lakh` columns.

14,828 raw rows -> **12,691 clean rows**.

## 4. Visualizations and Outcomes
| Graph | Outcome |
|---|---|
| `1_price_distribution.png` | Market is budget-heavy: median price is about **4.3 lakh**, and about **56%** of cars sell under 5 lakh. Distribution is right-skewed by a few premium cars. |
| `2_price_vs_year.png` | Newer cars are worth far more. Average price rises from about 0.7 lakh (1999 models) to over 25 lakh for 2021-22 models, with steepest growth after 2019. (Newest years have fewer, mostly premium listings, so they overstate the typical car.) |
| `3_top_brands.png` | **Maruti Suzuki** is the most listed brand (3,654 cars). Among the top 10, **Toyota** has the highest average price (about 10.4 lakh) and **Chevrolet** the lowest (about 2.6 lakh). |
| `4_fuel_transmission_boxplot.png` | Diesel cars have a higher median price (5.5 lakh) than petrol (3.25 lakh). Automatics (13 lakh median) are far pricier than manuals (3.85 lakh), but manuals are about **86%** of listings. |
| `5_km_vs_price.png` | More kilometres means lower price, but the link is moderate (correlation about -0.21). Car age (about -0.41) matters more than mileage. |

## 5. Libraries and Tools
- **Python 3**
- **pandas**: loading, merging, cleaning, grouping
- **numpy**: log transform, IQR outliers, trend line, correlation
- **matplotlib**: all five graphs
- Git and GitHub: version control and hosting

## 6. Project Structure
```
used-car-analysis/
├── README.md
├── requirements.txt
├── cleaning_log.txt
├── src/clean_and_analyze.py
├── data/raw/            (4 original CSVs)
├── data/cleaned/cleaned_cars.csv
└── graphs/              (5 PNG images)
```

## 7. How to Run
```bash
pip install -r requirements.txt
python src/clean_and_analyze.py
```

## 8. Limitations
- Data comes from different sources and years; prices are not adjusted for inflation.
- Duplicate removal is based on matching listing attributes, so a few genuine identical listings may be dropped.
- `car_age` is computed relative to 2026.

## 9. GitHub Link
https://github.com/<your-username>/used-car-analysis
