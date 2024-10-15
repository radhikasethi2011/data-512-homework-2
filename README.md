# data-512-homework-2

---

# DATA-512 Homework 2: Wikipedia Article Coverage on Politicians

## Overview

This project explores biases in Wikipedia's coverage of political figures by analyzing article counts and quality scores across countries and regions. The key goal is to understand how representative Wikipedia is globally when it comes to political coverage, using population data and article quality scores predicted by the ORES machine learning service.

Through merging two datasets—one containing Wikipedia articles about politicians and the other with country population data—this project calculates metrics like total articles per capita and high-quality articles per capita. The analysis provides insights into regional disparities in both the quantity and quality of Wikipedia's political content.

## Folder Structure

```
data-512-homework-2
│
├── code
│   └── data-collection.ipynb              # Main notebook containing data cleaning, analysis, and visualizations
│
├── data
│   ├── bottom_10_countries_by_coverage.csv      # Bottom 10 countries by total articles per capita
│   ├── bottom_10_countries_by_high_quality.csv  # Bottom 10 countries by high-quality articles per capita
│   ├── country_grouped_metrics.csv              # Grouped data at the country level with key metrics
│   ├── region_grouped_metrics.csv               # Grouped data at the regional level with key metrics
│   ├── regions_by_high_quality_coverage.csv     # Regions ranked by high-quality articles per capita
│   ├── regions_by_total_coverage.csv            # Regions ranked by total articles per capita
│   ├── top_10_countries_by_coverage.csv         # Top 10 countries by total articles per capita
│   ├── top_10_countries_by_high_quality.csv     # Top 10 countries by high-quality articles per capita
│   ├── ores_error_log.txt                       # Log file for any issues retrieving ORES predictions
│   ├── politicians_by_country_AUG.2024.csv      # Original Wikipedia politicians data
│   ├── politicians_with_quality.csv             # Politicians data with ORES quality scores
│   ├── population_by_country_AUG.2024.csv       # Population data
│   └── wp_countries-no_match.txt                # Countries unmatched between the two datasets
│
├── LICENSE
└── README.md

```

## Data Sources

- **Wikipedia Politicians Dataset**: A dataset containing articles related to politicians, including their country, article title, and ORES-predicted quality scores.
  
- **Population Dataset**: Population data sourced from the Population Reference Bureau (August 2024), with hierarchical regions to categorize countries.

## Methodology

### 1. Data Cleaning and Preprocessing
The initial step involved cleaning the Wikipedia and population datasets. This included standardizing country names and handling inconsistencies like duplicates or missing data. We merged both datasets using the country field as the key, and countries that couldn't be matched were logged separately.

### 2. Retrieving Article Quality Scores
Using the ORES API, we gathered quality predictions for each Wikipedia article in the dataset. Articles marked as "FA" (Featured Article) or "GA" (Good Article) were classified as "high quality." Any errors during retrieval were captured in `ores_error_log.txt`.

### 3. Merging Datasets
Once cleaned, both datasets were merged, with a focus on aligning the Wikipedia politicians' data with population figures. Countries not present in both datasets were logged, and only countries appearing in both were included in the final analysis.

### 4. Calculating Metrics
Two key metrics were calculated:
- **Total Articles per Capita**: The total number of Wikipedia articles about politicians per million people.
- **High-Quality Articles per Capita**: The number of high-quality articles per million people.

These metrics were calculated both at the country and regional levels to ensure a broader understanding of global disparities.

### 5. Ranking and Output
The key outputs of the analysis include:
- **Top 10 Countries by Coverage**: Countries with the highest total articles per capita.
- **Bottom 10 Countries by Coverage**: Countries with the lowest total articles per capita.
- **Top 10 Countries by High-Quality Articles**: Countries with the highest high-quality articles per capita.
- **Bottom 10 Countries by High-Quality Articles**: Countries with the lowest high-quality articles per capita.
- **Regions by Total Coverage**: Geographic regions ranked by total articles per capita.
- **Regions by High-Quality Coverage**: Geographic regions ranked by high-quality articles per capita.

### 6. Error Logging and Missing Data
We logged all articles that failed to retrieve a quality score from ORES in `ores_error_log.txt`. While the error rate was minimal, these logs were crucial for understanding any gaps in the data collection process. Here the error rate is 0.11%

## Results

The analysis outputs various ranked lists based on the metrics calculated. The key findings include:

- **Top 10 Countries by Coverage**: Countries like Antigua and Barbuda, Federated States of Micronesia, and Marshall Islands had the highest articles per capita, despite their small populations.
- **Bottom 10 Countries by Coverage**: Larger countries like China, India, and Saudi Arabia had low article coverage per capita.
- **Top 10 Countries by High-Quality Articles**: Montenegro, Luxembourg, and Albania ranked highest in high-quality articles per capita.
- **Bottom 10 Countries by High-Quality Articles**: Countries like China, Antigua and Barbuda, and Barbados had no high-quality articles per capita.

---

## Research Implications

### Expected Biases

Before diving into the data, I had a feeling that countries with larger English-speaking populations—like the U.S. or the U.K.—would have significantly more Wikipedia articles about politicians compared to other nations. It also seemed pretty likely that wealthier countries or those with more political influence would have higher-quality articles, while regions with lower internet penetration (such as Africa and Southeast Asia) would be underrepresented. 

### Biases Found During the Analysis

Several interesting biases surfaced during the project that highlighted some gaps in the data:

- **Geographic Disparities**: As expected, countries from Western Europe and Oceania led in terms of both article coverage and quality. For example, countries like Antigua and Barbuda and the Marshall Islands had the highest articles per capita, while Montenegro topped the list for high-quality articles per capita. On the other hand, countries like China, Ghana, and India were among those with the lowest articles per capita. This is a direct reflection of the broader digital divide.
  
- **Country Name Issues**: As I worked on merging the datasets, country name mismatches (e.g., "China" vs. "China (Hong Kong SAR)") created problems. Even regions like "North Korea" and "South Korea" couldn’t be easily combined without introducing bias, so I had to leave them out.

- **Small Population Bias**: Countries with tiny populations, like Antigua and Barbuda, ranked high for articles per capita, which skewed the rankings. While these countries have fewer articles, their small populations inflate the per capita metric, pushing them to the top of the list.

### Insights on Wikipedia's Data Bias

From the results, it’s clear that Wikipedia favors countries with larger internet user bases and greater access to digital resources. While the platform is open to contributors globally, regions with fewer active contributors—whether due to language barriers, limited internet access, or other factors—are underrepresented. This creates an imbalance, especially when performing country-level analyses, where richer nations or regions with higher internet engagement dominate.

### Reflections

The data shows that while Wikipedia is an amazing resource, it reflects the digital inequalities of our world. Countries with better internet access and more active contributors naturally end up with more and better-quality articles. If we want a more balanced representation, there needs to be a push towards getting more people from underrepresented regions to contribute.

---

## Results

- **Top 10 Countries by Total Articles per Capita**: Countries like *Antigua and Barbuda* and *Federated States of Micronesia* led in total articles per capita. These nations, though small in population, have relatively higher Wikipedia coverage when normalized by population size.
  
- **Bottom 10 Countries by Total Articles per Capita**: Larger nations such as *China*, *India*, and *Ghana* were ranked low in total articles per capita. Despite their significant populations, they had fewer articles per person.

- **Top 10 Countries by High-Quality Articles per Capita**: Countries like *Montenegro* and *Luxembourg* had the highest proportion of high-quality articles (classified as FA or GA). This suggests that although these countries may not have a high number of total articles, their article quality is comparatively strong.

- **Bottom 10 Countries by High-Quality Articles per Capita**: Several countries, including *Antigua and Barbuda*, *Barbados*, and *China*, had no high-quality articles per capita, indicating an area where more contributions are needed.

- **Geographic Regions by Total Coverage**: *Northern Europe* and *Oceania* stood out with the highest total articles per capita, reflecting greater political coverage in these regions. On the other hand, *South Asia* and *East Asia* were at the lower end of the spectrum.

- **Geographic Regions by High-Quality Coverage**: Regions like *Southern Europe* and *Northern Europe* led in high-quality articles per capita, showing a higher concentration of top-quality content. *South Asia* and *East Asia* were again among the lowest-ranked regions.

---

## Conclusion

This project was a deep dive into how Wikipedia covers politicians across the globe, revealing some key challenges in working with large datasets and how they reflect global inequalities. One of the biggest takeaways for me was just how important it is to maintain consistency when merging datasets, especially when dealing with different country names or missing population data. It was clear that discrepancies in the data—like country name mismatches and zero population entries—directly influenced the results, impacting the accuracy of the per capita metrics.

Another big learning moment was realizing how much data cleaning impacts the final analysis. I spent a lot of time making sure the datasets aligned, and it became clear that small mistakes in this step can snowball into bigger issues later on. On top of that, the choice of unit measurement, like using millions for population, really matters for producing meaningful results. Without that, certain countries’ coverage could look artificially inflated or deflated.

Overall, the project emphasized the need for standardized processes and better data documentation in future research. Having clear, well-documented methods for scraping and cleaning data will help avoid introducing unintended bias in future analyses. In the end, this project not only highlighted global digital disparities, but it also showed how these biases can influence the results when analyzing datasets at a global scale.

---

## More Details on API Usage

In this project, we used the [MediaWiki API](https://www.mediawiki.org/wiki/API:Main_page) to collect metadata like revision IDs for each politician's article. This step was crucial for retrieving up-to-date quality predictions using ORES, Wikipedia's machine learning service. If you're curious about how this works, the [API:Info](https://www.mediawiki.org/wiki/API:Info) documentation is a good starting point. It covers all the details on how to request info for specific Wikipedia pages.

The ORES API was another essential tool for determining article quality. It uses machine learning models to predict an article's quality based on factors like its structure and content. This allowed us to classify articles as "FA" (Featured Article), "GA" (Good Article), or lower quality. You can check out the [ORES documentation](https://www.mediawiki.org/wiki/ORES) for more details on how these predictions work.

---

## References

- Wikipedia API: [https://www.mediawiki.org/wiki/API:Main_page](https://www.mediawiki.org/wiki/API:Main_page)
- ORES API Documentation: [https://www.mediawiki.org/wiki/ORES](https://www.mediawiki.org/wiki/ORES)
- Population Data Source: United Nations Population Database (August 2024)
- Creative Commons License (Code Example by Dr. David W. McDonald): [https://creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/)
---



## License 
This project is licensed under the [MIT License](LICENSE). 
For more information, you can find the full license text in the LICENSE file included in this repository.

