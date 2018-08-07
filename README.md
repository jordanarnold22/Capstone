# NBA Free Agent Salary Predictor

“There is an epidemic failure within the game to understand what is really happening. This leads people who run Major League Baseball teams to misjudge their players and mismanage their teams.”
  							                - Jonah Hill (Moneyball, 2011)

Moneyball and sabermetrics has opened the door for analytics to enter the sports world in a big way. Every sport at this point has been infiltrated by data analytics to some degree which has allowed teams to make more informed decisions about what the keys to success really are, what players will help them achieve success, and what these players are worth. Teams that are on the forefront of the analytics movement are clearly reaping the benefits as we can currently see with teams like the Houston Rockets and the Boston Celtics. Making analytics based decisions can set a team up for years and years of success, while avoiding this trend and sticking to the eye test can drastically decrease a team's chances of longterm success. I trained a model to predict the salary for an NBA free agent for the first year of their new contract.

## Getting the Data

I used BeautifulSoup to scrape standard and advanced statistics from www.basketball-reference.com for every player that has played in the NBA since 2012. I then scraped Wikipedia for lists of free agents every year since 2012. I also got historical NBA injury data from a Kaggle user. With all of these statistics I created a new dataframe that contained every free agent since 2012 as well as their statistics from the year before they hit the free agency market. With the injury data I noticed that there were 3 types of lower body tears that affected a player's salary the most (ACL, Achilles, meniscus). I also noticed that a player's salary would drastically decrease for each additional tear. Because of this I created a feature that summed the amount of ACL, Achilles, and meniscus tears that each player had at the time of their free agency. I then took each of these sums to the power of 10 to account for the multi-tear drop that I had seen in the data.

## Modeling

For my modeling process I tried several different algorithms. I ran my data through a neural network using Keras, I used a random forest regressor, a knn regressor, and several others. The model that gave me the best results was a simple linear regression. The disadvantage of using a linear regression here is that I could theoretically predict that a player would make less than the minimum salary or more than the maximum. Luckily this happened in very few cases. I went back and forth on whether or not I should do this, but I did end up setting each predictions to the minimum if it was below the NBA minimum and I did the same for the maximum. This improved my RMSE by about $150,000.

## Results

RMSE: $1,890,876.79
r2: .783

Considering the amount of outliers that I had, I am very happy with an RMSE of just under $1.9M. There are some aspects of NBA free agency that are difficult to put into a model. For example, I was about $6.5M off on Kevin Durant's 2017-18 contract. He took less money at this time so that the Warriors could also re-sign some key role players. Another outlier was Dwight Howard's 2018-19 contract which I was around $15M off. It was difficult to put a player's awful relationships with past teams or a player deciding to less money than he deserves into the model, however these are problems that I am currently trying to navigate.

## Next Steps

At this point I am just predicting a player's first year salary for the contract that they sign during free agency. The next steps will be to predict the length of each contract, the type of each contract (Bird rights, mid-level exception, etc...), and player movement to and from the G league and foreign leagues. The ultimate goal is to create a multi-class classification that will predict where each free agent ends up.
