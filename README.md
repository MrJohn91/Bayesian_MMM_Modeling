# Bayesian Mixed-Media Model (MMM) Marketing Analysis

## Project Overview
This project applies a Bayesian Mixed-Model to analyze marketing spend effectiveness across seven different advertising channels. The analysis identifies which channels drive the most revenue, measures their return on investment (ROI), and quantifies how marketing effects carry over to future weeks.

## Objectives

The main objectives were to:
1. Model the carryover effect of marketing spend
2. Identify the most and least effective marketing channels
3. Calculate channel-specific ROI values
4. Understand seasonal patterns in revenue
## Technologies Used
- **Python 3.x**: Programming language 
- **PyMC**: For Bayesian modeling and MCMC sampling
- **Pandas & NumPy**: For data manipulation and computational work
- **Plotly, Seaborn and Matplotlib**: For interactive data visualization
- **Google Colab**: For model desiging and execution

## Key Findings

### Channel Effectiveness
![Channel Coefficients](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/Channel%20Coefficient.png)
This visualization shows the effectiveness of each marketing channel. Channels 6, 5, 7, and 3 show positive effects, with Channel 6 being the most effective (generating €2.05 for every €1 spent). Channels 1, 2, and 4 show negative effects on revenue.
### Return on Investment (ROI)
![ROI by Channel](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/ROI%20by%20channel.png)
This chart displays the return on investment for each marketing channel. Channel 6 has the highest ROI at 2.56 (156% return), while Channel 2 has the lowest at -15.41, likely due to the very low spend in that channel. Four channels show positive ROI, while three channels have negative returns.
### Total Revenue Contribution
![Contributions by Channel](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/Contributions%20by%20channel.png)
This chart displays the total revenue contribution from each channel. Channel 7 makes the largest absolute contribution (€3.98M) despite not having the highest effectiveness coefficient, due to its higher spending levels.
### Model Fit
![Model Fit](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/Model%20fit.png)
The model achieves an R² of 0.583, explaining 58.3% of the variance in weekly revenue. The red line shows predicted revenue closely tracking actual revenue (blue dots).

### Revenue Decomposition
![Revenue Decomposition](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/Revenue%20Decomposition.png)
This visualization breaks down revenue into its key components, revealing several important insights:

- **Total Revenue (top panel)**: Shows clear spikes in January 2021 and January 2022, with revenue typically fluctuating throughout the year. The overall pattern suggests some revenue volatility with a gradual decline over the two-year period.

- **Trend Component (second panel)**: Reveals a consistent downward trend in the business. This decline represents a strategic challenge requiring attention.

- **Seasonal Component (third panel)**: Identifies regular cyclical patterns throughout the year that repeat predictably regardless of marketing activities. The magnitude of these seasonal effects is relatively small compared to special event effects.

- **Special Event Effects (bottom panel)**: Quantifies the substantial impact of key periods, with November (Black Friday or Cyber Monday) showing the strongest positive effect, followed by January with a moderate positive effect. This suggests customers concentrate purchases during Black Friday sales and may delay some December purchases until January.

The model clearly isolates how much of the business performance is driven by long-term trends versus seasonal patterns versus specific retail events, allowing for more targeted marketing strategies.

## Challenges & Solutions

### Technical Challenges
- **PyMC Installation**: Encountered dependency conflicts in the local environment, resolved by switching to Google Colab
- **Model Convergence**: Initial models showed poor fit, improved by implementing channel-specific adstock parameters
- **Outlier Management**: Extreme revenue spikes required special handling with explicit holiday indicators
### Analytical Challenges
- **Negative Coefficients**: Several channels showed counterintuitive negative effects, requiring careful interpretation
- **Optimal Decay Rates**: Finding the best adstock parameters required testing multiple values for each channel
- **Seasonality Modeling**: Discovered that modeling November explicitly was crucial for capturing Black Friday effects and Cyber Monday

## Answering Key Questions

### How do model spend carry over?
By implementing channel-specific geometric adstock transformations. For each channel, i tested decay rates between 0.1-0.9 and selected the optimal value that maximized correlation with revenue. This approach recognizes that different channels have different patterns of delayed impact.
### Explaining choice of prior inputs to the model
using weakly informative priors that provide some regularization while allowing the data to drive the findings. For channel coefficients, i used Normal(0, 10) priors, allowing for both positive and negative effects with a wide enough range to accommodate realistic marketing impacts.
### How the model results based on prior sampling vs. posterior sampling?
The posterior distributions are substantially narrower than the priors, indicating that the data significantly updated our initial beliefs. For example, the posterior for Channel 6's coefficient narrowed to a range of 1.98-2.11, with a mean of 2.05, compared to the much wider prior.
### How good is the model performing? How do you measure it?
The model performs well with an R² of 0.583, explaining 58.3% of the variance in revenue. Indicating that the model captures meaningful patterns in the data. For a marketing mix model, an R² above 0.5 is generally considered a good fit.

Additional metrics include:
- MAPE (Mean Absolute Percentage Error) of 17.34% – This means our revenue predictions are, on average, about 17% off compared to actual numbers. For every €100 in revenue, we might be off by around €17 higher or lower.
- MAE (Mean Absolute Error) of €23,079 – On average, our predictions differ from actual revenue by about €23,000 per week. Some weeks we're slightly under, some slightly over, but that’s the typical gap.
### Main insights in terms of channel performance/effects?
The analysis revealed that Channels 6, 5, and 7 are effective at driving revenue, while Channels 1, 2, and 4 show negative associations with revenue. We also found strong seasonal effects, particularly in November (Black Friday) and January (post-holiday).
### Deriving ROI estimates per channel? What is the best channel in terms of ROI?
Channel 6 provides the best ROI at 2.56 (156% return), followed by Channel 5 at 1.71 (71% return) and Channel 7 at 1.38 (38% return). Channels 1, 2, and 4 show negative ROI, suggesting marketing spend should be reallocated away from these channels.

## Next Steps & Improvements

### Model Improvements
-  Trying more advanced adstock models to better capture how marketing effects build up and fade over time.
-  Checks if channels work together by exploring how they might boost each other’s impact.
-  Use cross-validation to test the model on different data sets and make sure it holds up well

### Business Applications
- Develop an optimal budget allocation strategy based on channel ROI
- Create a dashboard for ongoing monitoring of channel performance
- Design channel-specific seasonal strategies to capitalize on November/January effects

### Data Enhancements
- Incorporate competitor activity data if available
- Include details about sales and discounts to see their impact
- Collect and analyze customer segment data to understand channel effectiveness by audience
