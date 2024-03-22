# LOLAnalysis2018
This is a repository about League of Legends 2018 data analysis 

<h1>Strategic Early Decisions and Their Impact on Victory in League of Legends</h1>

## Introduction

<p>In the competitive realm of professional League of Legends, the actions taken in the early stages of a game can often determine the outcome of the entire match. This analysis probes into the 2018 season's professional matches to extract valuable insights into how early-game performances correlate with the chances of winning.</p>

<p>Our analysis, fueled by data sourced from Oracle's Elixir, scrutinizes the importance of achieving 'First Blood,' capturing dragons, and destroying the first tower. These key objectives are crucial for gaining early control and setting a precedent for the rest of the match.</p>

<p>Our project pivots around one central question: "How do early-game achievements, such as securing 'First Blood', capturing dragons, and destroying the first tower, affect a team's chances of victory?"</p> 
  
<p>We concentrate on several vital metrics that shape our understanding of a match's dynamics:</p>

<ul>
  <li><b>gameid:</b> Acts as the linchpin for our analysis, uniquely identifying each match.</li>
  <li><b>side:</b> Offers context on the starting position, which may influence the strategy for securing First Blood.</li>
  <li><b>firstblood:</b> A significant early game event that can provide both psychological and strategic advantages.</li>
  <li><b>dragons:</b> Reflects the control over neutral objectives that a team possesses.</li>
  <li><b>firsttower:</b> Signifies the initial step towards territorial dominance and map control.</li>
  <li><b>gamelength:</b> Provides a narrative on how the game's strategy played out and the ability of a team to conclude the match effectively.</li>
</ul>

<p>With a dataset of 11,559 matches post-data cleaning, our research aims to go beyond academic analysis. We aspire to identify the key early-game objectives that play a critical role in securing victory. This research can guide players and teams in enhancing their strategic play within League of Legends.</p>


## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

Our analysis began by loading the dataset and filtering for complete data to ensure the validity of our analysis. We distinguished between team-level data and player-level data and focused on the team-level metrics that are crucial for our investigation. During our data cleaning process, we converted categorical data into boolean and category types for clearer analyses and handled missing values by dropping columns with more than 50% missing data. The cleaning steps were essential in focusing our analysis on the most impactful factors that may affect a team's win rate.

![Head of Cleaned DataFrame](assets/head_cleaned_dataframe.png)

### Univariate Analysis

Our univariate analysis revealed interesting patterns in the distribution of dragons secured by teams throughout the matches. Here is a bar chart that shows the distribution of dragons secured by teams:

<iframe src="assets/dragons_distribution.html" width="800" height="600" frameborder="0"></iframe>

This bar chart illustrates the percentage of games in which teams secured a varying number of dragons, providing insights into common dragon control strategies.

### Bivariate Analysis

Next, we examined the relationship between securing objectives like dragons and first towers and the final match result. Our analysis demonstrated that teams securing these objectives have a higher probability of winning their matches.

<iframe src="assets/dragons_winrate.html" width="800" height="600" frameborder="0"></iframe>

This stacked bar chart shows that securing more dragons is often associated with an increased win rate, underscoring the strategic importance of dragon control.

<iframe src="assets/firsttower_winrate.html" width="800" height="600" frameborder="0"></iframe>

Similarly, the team that destroys the first tower generally has a better chance of winning, as indicated by the stacked bar chart above.

### Interesting Aggregates

Finally, our exploration of aggregated data, such as the average number of dragons secured in wins versus losses, provided further evidence of the link between early-game objectives and match outcomes.

## Assessment of Missingness

<p>We evaluated the dataset for non-trivial missingness and hypothesized whether certain features might be NMAR (Not Missing At Random). Our focus was on the <em>split</em> column. A permutation test revealed that its missingness significantly depends on the <em>playoffs</em> column, suggesting a potential NMAR scenario, as there was a non-zero correlation with a p-value of 0.0. This might imply that the data is missing systematically related to whether the match was part of the playoffs.</p>

<p>In contrast, no dependency was found between the missingness of <em>split</em> and <em>golddiffat15</em>, indicated by a zero correlation and a p-value of 1.0. Therefore, missingness in the <em>split</em> column appears to be random with respect to <em>golddiffat15</em>, likely MAR (Missing At Random).</p>

<p>To further validate these findings, it would be beneficial to gather additional information on the data collection process, specifically during the playoffs period, to understand why missingness occurs in the <em>split</em> column.</p>


<hr>

## Hypothesis Testing

<p>In our hypothesis testing, we examined the effect of securing early game objectives on the winning rate of the game. The observed statistic represents the mean difference in the win rate between games with an early game score greater than 0 and those with a score of 0, which was approximately 0.496. With a p-value of 0.0, the result is statistically significant, leading us to reject the null hypothesis and accept the alternative hypothesis that securing early game objectives increases the winning rate of the game.</p>

<hr>

## Framing a Prediction Problem

<p>For our prediction problem, we chose a binary classification to predict the outcome of matches, focusing on early game metrics such as 'firstblood', 'firsttower', 'dragons', and 'gamelength'. We justified 'result' as the response variable because it is the ultimate outcome of a game and is directly influenced by early game performance. The F1-score was chosen as the evaluation metric for its balance of precision and recall, which is crucial in a competitive environment where minimizing false positives and negatives is equally important.</p>

<p>Our model aims to predict the outcome of matches using features available at the time of prediction, ensuring no look-ahead bias in our approach. The final model's accuracy and balanced F1-score suggest that the features selected for training are indicative of a team's likelihood of winning, underscoring the strategic value of early game achievements in League of Legends.</p>


## Baseline Model

<p>For the baseline model, we implemented a pipeline using one-hot encoding for categorical features 'firstblood' and 'firsttower', and no transformation for numerical features 'dragons' and 'gamelength'. The pipeline includes a logistic regression classifier with increased max iterations for better convergence. This baseline model yielded an accuracy score of approximately 0.769 on the test set, suggesting that about 76.9% of the model’s predictions were accurate.</p>

## Final Model

<p>The final model, created with a RandomForestClassifier, underwent hyperparameter tuning through GridSearchCV. Post-tuning, the model demonstrated a slight improvement with an accuracy score of 0.7722273143904674, hinting at the positive impact of feature engineering and hyperparameter optimization. The key hyperparameters were {'classifier__max_depth': 5, 'classifier__n_estimators': 400}, indicating a depth-constrained, but ensemble-rich model.</p>

## Fairness Analysis

<p>In assessing fairness, I posed the question: "Does our model perform equally well for teams starting on the Blue side as it does for teams on the Red side?" I conducted a permutation test to compare the RMSE between the two groups. The observed RMSE difference was -0.0078 with a p-value of 0.263. Since the p-value exceeded the conventional alpha level of 0.05, we did not find substantial evidence to declare the model biased. The analysis suggests the model's performance is fair concerning RMSE between the Blue and Red sides.</p>


