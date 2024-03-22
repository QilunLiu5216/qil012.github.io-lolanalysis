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





