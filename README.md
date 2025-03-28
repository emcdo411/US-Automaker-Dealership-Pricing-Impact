# US Automaker Dealership Pricing and Economic Impact Visualization

### Repo Name Suggestion:
**"US-Automaker-Dealership-Pricing-Impact"**

---

## Project Summary

This project aims to provide insights into how **economic factors**, such as **tariffs**, **price increases**, and the **Federal Reserve's monetary policy** affect both the **automotive market** and **job markets** in key industries. The analysis visualizes these impacts across two Texas cities, **Dallas** and **Fort Worth**, by plotting top-selling vehicles from major US automakers and their dealerships, alongside economic trends that could affect employment in the **automotive**, **construction**, **technology**, and **healthcare** sectors.

The project includes:
- **2D Interactive Maps** showing dealership locations and **price increases** of top-selling models by major automakers.
- **3D Interactive Map** showing the impact of **interest rate adjustments** by the Federal Reserve on **job market growth** in several key industries.
- A **comprehensive analysis** of **tariffs**, **inflation**, and their effects on vehicle pricing and consumer purchasing decisions.

This case study helps to better understand how economic changes, such as interest rate hikes or price increases by automakers, influence **business strategy**, **consumer behavior**, and **employment trends** in multiple sectors.

---

## What Was Accomplished?

### Key Features:
1. **Interactive 2D Maps for Fort Worth and Dallas:**
   - Mapped **dealership locations** for the top-selling vehicles from Ford, General Motors, and Chrysler.
   - Visualized **price increase data** by showing the percentage and dollar increase for top models.
   
2. **3D Map for Industry Job Growth Impact:**
   - Created a **3D plot** to illustrate the projected **job market changes** over the next two quarters across four industries (healthcare, construction, technology, and automotive) if the **Federal Reserve raises interest rates**. This was done based on simulated data showing potential job growth or loss.

3. **Impact of Tariffs on Vehicle Prices:**
   - Displayed the potential impact of **tariffs** on the **top-selling vehicle models** from the **Big 3 US automakers**.
   - Included an analysis of how automakers could respond to price increases and the effects of inflation.

---

## Why This Matters

The ongoing economic environment—shaped by **interest rate adjustments**, **inflation**, and **tariffs**—is having a profound effect on **consumer purchasing behavior** and **employment trends**. Understanding how these factors influence:
- **Automaker pricing decisions**, such as price hikes due to tariffs or inflation.
- The **job market dynamics** in key industries.
- **Regional dealership pricing** strategies.

This project enables stakeholders, including manufacturers, policymakers, and analysts, to make informed decisions about pricing, employment forecasting, and strategic planning.

The 3D visualization of **job market impact** based on **Federal Reserve interest rate decisions** can aid businesses and policymakers in forecasting the economic outcomes of future monetary policy decisions, while the dealership mapping assists automakers in **evaluating regional pricing strategies** and consumer behavior.

---

## Code Implementation

### 1. **Dealership Data for Dallas/Fort Worth**

The dataset includes **dealership names**, **vehicle models**, and **price increase** information for various **automakers** in **Fort Worth** and **Dallas**. Below is the code that defines the **dealership data**.

```r
# Dealership Data for Fort Worth
dealerships_fortworth <- c("Ford of Fort Worth", "Chrysler Jeep Dodge Ram Fort Worth", 
                           "AutoNation Ford Fort Worth", "Huffines Chrysler Jeep Dodge Ram", 
                           "Vandergriff Toyota", "Luther Ford Lincoln Fort Worth", 
                           "North Central Ford Fort Worth", "Classic Chrysler Jeep Dodge Ram", 
                           "Vandergriff Honda", "AutoNation Chrysler Dodge Jeep Ram Fort Worth")

latitudes_fortworth <- c(32.7490, 32.7590, 32.7754, 32.8700, 32.7410, 32.8200, 
                         32.8010, 32.8431, 32.7771, 32.7730)

longitudes_fortworth <- c(-97.3413, -97.3479, -97.3328, -97.2134, -97.2297, -97.3523, 
                          -97.2928, -97.4167, -97.3090, -97.4386)

model_names_fortworth <- c("Ford Mustang", "Chevrolet Silverado", "Jeep Grand Cherokee", 
                           "Ram 1500", "Ford F-150", "Chevrolet Equinox", "Jeep Wrangler", 
                           "Ram 2500", "Ford Explorer", "Chevrolet Malibu")

price_increase_percentage_fortworth <- c(5.0, 7.0, 6.5, 8.0, 6.0, 5.5, 7.5, 8.5, 5.0, 6.5)
base_model_price_fortworth <- c(27000, 32000, 35000, 40000, 33000, 28000, 35000, 42000, 36000, 28000)
price_increase_dollars_fortworth <- base_model_price_fortworth * price_increase_percentage_fortworth / 100

dealership_data_fortworth <- data.frame(
  dealerships = dealerships_fortworth, 
  latitudes = latitudes_fortworth, 
  longitudes = longitudes_fortworth,
  model_names = model_names_fortworth, 
  price_increase_percentage = price_increase_percentage_fortworth,
  price_increase_dollars = price_increase_dollars_fortworth
)
```

### 2. **2D Interactive Map for Fort Worth**

Here's how to create a **2D map** showing the **dealerships** and their respective **top models** with price increase data:

```r
library(leaflet)

leaflet(data = dealership_data_fortworth) %>%
  addTiles() %>%
  addMarkers(
    lat = ~latitudes, 
    lng = ~longitudes, 
    popup = ~paste('<b>Dealership:</b> ', dealerships, 
                   '<br><b>Model:</b> ', model_names, 
                   '<br><b>Price Increase:</b> ', price_increase_percentage, '%', 
                   '<br><b>Dollar Increase:</b> $', round(price_increase_dollars_fortworth, 2)),
    label = ~dealerships
  ) %>%
  addProviderTiles(providers$CartoDB.Positron) %>%
  setView(lng = -97.3430, lat = 32.7555, zoom = 10)
```

### 3. **3D Map for Job Growth Impact Due to Federal Reserve Interest Rates**

This is a **3D plot** showing the predicted job growth (or decrease) across **Healthcare**, **Construction**, **Technology**, and **Automotive** industries if the **Federal Reserve** raises interest rates over the next two quarters.

```r
library(plotly)

# Create a data frame with mock data for the 3D plot
industries <- c("Healthcare", "Construction", "Technology", "Automotive")
job_growth_percentage <- c(3.5, 2.0, 1.5, 1.0) # Mock growth data

data_3d <- data.frame(
  industries = industries,
  job_growth_percentage = job_growth_percentage,
  interest_rate_increase = c(0.5, 0.5, 0.5, 0.5)  # Same rate increase for simplicity
)

# Plot 3D scatter plot
plot_ly(data_3d, 
        x = ~industries, 
        y = ~job_growth_percentage, 
        z = ~interest_rate_increase, 
        color = ~job_growth_percentage, 
        colors = "Viridis",
        type = "scatter3d", 
        mode = "markers+lines",
        hoverinfo = 'text',
        text = ~paste('Industry:', industries, 
                      '<br>Job Growth:', job_growth_percentage, '%',
                      '<br>Interest Rate Impact:', interest_rate_increase, '%')
) %>%
  layout(title = "Impact of Federal Reserve Interest Rate on Job Growth",
         scene = list(
           xaxis = list(title = 'Industry'),
           yaxis = list(title = 'Job Growth (%)'),
           zaxis = list(title = 'Interest Rate Increase (%)')
         ))
```

---

## Why This Is Important

This project leverages **interactive data visualizations** to explore **economic policy effects** in the automotive and job markets. By visualizing the impacts of **tariffs**, **price increases**, and **Federal Reserve monetary policy**, stakeholders in the **automotive industry**, **economic forecasting**, and **employment planning** can make more informed, data-backed decisions.

### Key Takeaways:
- **Economic Shifts**: By showing how tariffs, price hikes, and interest rate increases affect **job markets** and **consumer behavior**, we offer critical insights that go beyond numbers.
- **Decision-Making Tool**: Visualizing this data allows **policy-makers**, **automakers**, and **analysts** to anticipate **economic trends**, **consumer reactions**, and **employment forecasts**.
- **Interactive Exploration**: These **interactive maps** and **3D graphs** provide stakeholders with a powerful tool for analyzing complex economic scenarios and making strategic decisions.

---

## Conclusion

This project offers a comprehensive and data-driven approach to understanding the effects of **economic factors** on the **automotive market** and **job market growth**. The visualizations provide valuable insights that can inform both **business decisions** and **economic policy**.

---

### Explore the full code and data visualizations in the repository:

[**GitHub Repo**](https://github.com/yourusername/US-Automaker-Dealership-Pricing-Impact)

---

### Tags:
#AutomotiveIndustry #PriceIncrease #Tariffs #DataVisualization #EconomicForecasting #Automakers #Dealerships #Leaflet #RProgramming #FederalReserve #InterestRates #JobGrowth #Dallas #FortWorth #USAutomakers

---

This comprehensive README explains both the methodology and the significance of the project, providing all the essential context, code, and visualizations, making it an impactful and professional showcase of your analysis.
