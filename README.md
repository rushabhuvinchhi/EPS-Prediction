# EPS-Prediction
Predicting earnings per share and trading on earnings surprise

The architecture consists of the three parts: Prediction Phase, Exploratory Phase and Portfolio Construction phase:

## Prediction Phase
This phase was almost entirely done by the previous group. However, we have added a GridSearch module to this phase. This module basically tries all the combinations of parameters of the Machine Learning Model that gives us the best validation error in prediction. Because of this module, we were able to improve the R squared metric of the prediction from the existing model. This metric basically tells us how well our ML model is doing in its predicting task.

## Exploratory Phase
This phase was newly implemented by our group to obtain more fundamental indicators that we can successfully predict. For this, we started off with a list of candidate fundamental indicators for each stock. Using the existing data, we used Machine Learning to predict each of these candidates. By a combination of eye balling and the R squared metric score, we selected the final three fundamental indicators that the Machine Learning model was able to predict with a very high accuracy.

The candidate list: Return on Assets (ROA), Return on Equity (ROE), Efficiency Ratio, Dividend Yield, Cash Deposits, Free Cash Flow (FCF) etc.

## Portfolio Construction
Now that we have predictions on EPS, ROA, FCF and ROE we wish to construct a portfolio of the universe of stocks that can make use of this information to maximise returns in the stock market. 

For this, we included another feature in this phase called the recency ratio[3 ]. According to this theory, analysts overweight recent low or high earnings. We can use this recency bias to add more weight to a stock that has recently posted low earnings because all the analysts would tend to give a conservative forecast. However, our Machine Learning model is free from such bias and thus can exploit this opportunity to make substantial gains from the surprise in earnings. 

The recency ratio, according to the study can be quantified as:

rr = 1 - (number of days since 52 week high / 2520)

The higher the ratio, more the stock weight should be.

Having all this information, we came up with the following simple model to construct weights.

    For the ith stock we have:
    
    Mi = epsi + (roai/10) + (roei/10) + (fcfi /10)+rr 
    
Here eps, roa, roe and fcfdenote surprises in the respective fundamentals that we have     predicted in contrast to existing perceptions in the market (analyst predictions).

After we have Miwe can construct the weight of each stock Wi as:

Wi = Mi / ∑Mi

## Instructions to run the code

1. Download the data and the code, ideally in one folder.
2. Run the 'TargetSelction.ipynb' to get additional predictions besides EPS.
3. Run the 'PortfolioConstruction.ipynb' to create tradeable portfolios. 
4. The code automatically generates diagnostic files to analyse return on portfolio, weight distributions of each stock before and after rebalancing and information ratios.
