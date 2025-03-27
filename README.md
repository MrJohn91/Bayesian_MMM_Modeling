# Bayesian Mixed-Media Model (MMM) Marketing Analysis
## Project Overview
This project applies a Bayesian Mixed-Media Model to analyze marketing spend effectiveness across seven different advertising channels. The analysis identifies which channels drive the most revenue, measures their return on investment (ROI), and quantifies how marketing effects carry over to future weeks.
## Objectives
The main objectives were to:
1. Model the carryover effect of marketing spend
2. Identify the most and least effective marketing channels
3. Calculate channel-specific ROI values
4. Understand seasonal patterns in revenue
## Technologies Used
- **Python 3.x**
- **PyMC**: For Bayesian modeling and MCMC sampling
- **Pandas & NumPy**: For data manipulation and computational work
- **Plotly**: For interactive data visualization
- **Google Colab**: For model desiging and execution
## Key Findings
### Channel Effectiveness
![Channel Coefficients](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/Channel%20Coefficient.png)
This visualization shows the effectiveness of each marketing channel. Channels 6, 5, 7, and 3 show positive effects, with Channel 6 being the most effective (generating €2.05 for every €1 spent). Channels 1, 2, and 4 show negative effects on revenue.
### Return on Investment (ROI)
![ROI by Channel](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/ROI%20by%20channel.png)
This chart displays the return on investment for each marketing channel. Channel 6 has the highest ROI at 2.56 (156% return), while Channel 2 has the lowest at -15.41. Four channels show positive ROI, while three channels have negative returns.
### Total Revenue Contribution
![Contributions by Channel](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/Contributions%20by%20channel.png)
This chart displays the total revenue contribution from each channel. Channel 7 makes the largest absolute contribution (€3.98M) despite not having the highest effectiveness coefficient, due to its higher spending levels.
### Model Fit
![Model Fit](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/Model%20Fit.png)
The model achieves an R² of 0.582, explaining 58.2% of the variance in weekly revenue. The red line shows predicted revenue closely tracking actual revenue (blue dots). This level of fit is considered good for marketing mix models, where many external factors beyond marketing can influence sales.
### Revenue Decomposition
![Revenue Decomposition](https://github.com/MrJohn91/Bayesian_MMM_Modeling/blob/main/Screenshots/Revenue%20Decomposition.png)
This visualization breaks down revenue into its components:
- Total revenue (top panel)
- Downward trend over time (second panel)
- Seasonal patterns (third panel)
- Holiday effects for November, December, and January (bottom panel)
## Challenges & Solutions
### Technical Challenges
- **PyMC Installation**: Encountered dependency conflicts in the local environment, resolved by switching to Google Colab
- **Model Convergence**: Initial models showed poor fit, improved by implementing channel-specific adstock parameters
- **Outlier Management**: Extreme revenue spikes required special handling with explicit holiday indicators
### Analytical Challenges
- **Negative Coefficients**: Several channels showed counterintuitive negative effects, requiring careful interpretation
- **Optimal Decay Rates**: Finding the best adstock parameters required testing multiple values for each channel
- **Seasonality Modeling**: Discovered that modeling November explicitly was crucial for capturing Black Friday effects and Cyber Monday
## Answers to Key Questions
### How do model spend carry over?
By implementing channel-specific geometric adstock transformations. For each channel, i tested decay rates between 0.1-0.9 and selected the optimal value that maximized correlation with revenue. This approach recognizes that different channels have different patterns of delayed impact.
### Explaining choice of prior inputs to the model
using weakly informative priors that provide some regularization while allowing the data to drive the findings. For channel coefficients, i used Normal(0, 10) priors, allowing for both positive and negative effects with a wide enough range to accommodate realistic marketing impacts.
### How the model results based on prior sampling vs. posterior sampling?
The posterior distributions are substantially narrower than the priors, indicating that the data significantly updated our initial beliefs. For example, the posterior for Channel 6's coefficient narrowed to a range of 1.98-2.11, with a mean of 2.05, compared to the much wider prior.
### How good is the model performing? How do you measure it?
The model performs well with an R² of 0.582, explaining 58.2% of revenue variance. Additional metrics include MAPE of 17.34% and MAE of €23,079. For marketing mix models, R² values above 0.5 are generally considered good.
### Main insights in terms of channel performance/effects?
The analysis revealed that Channels 6, 5, and 7 are effective at driving revenue, while Channels 1, 2, and 4 show negative associations with revenue. We also found strong seasonal effects, particularly in November (Black Friday) and January (post-holiday).
### Deriving ROI estimates per channel? What is the best channel in terms of ROI?
Channel 6 provides the best ROI at 2.56 (156% return), followed by Channel 5 at 1.71 (71% return) and Channel 7 at 1.38 (38% return). Channels 1, 2, and 4 show negative ROI, suggesting marketing spend should be reallocated away from these channels.
## Next Steps & Improvements
### Model Refinements
- Test more complex adstock functions that better capture how marketing effects rise and decay
- Explore interaction effects between channels to identify potential synergies
- Implement cross-validation to further validate model robustness

### Business Applications
- Develop an optimal budget allocation strategy based on channel ROI
- Create a dashboard for ongoing monitoring of channel performance
- Design channel-specific seasonal strategies to capitalize on November/January effects

### Data Enhancements
- Incorporate competitor activity data if available
- Include details about sales and discounts to see their impact
- Collect and analyze customer segment data to understand channel effectiveness by audience
