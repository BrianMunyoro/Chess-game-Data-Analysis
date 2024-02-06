# Online Chess Analysis

### Project Overview
This  is a comprehensive analysis of the  online chess. Using data obtained from Kaggle I analyzed various aspects of the game including  total games played, most common victory status and most common opening. SQL was used for both data querying and analysis

### Data Source
Chess games, Data source source used for this analysis is the chess_games.csv found on kaggle

### Tools

 - Excel
 
 - SQLlite for data analysis
 ### Exploratory Data Analysis
 EDA involved in exploring chess_games data to answer the following key questions:
 
 1. How many games in total were played?
 2. How many games contributed points?
 3. Which were the most common victory status
 4. Which were the most frequent opening moves?
 5. Average moves per game
 6. Highest rating between black and white
 7. Players with the most wins between black and white

###  Data Analysis
~~~ sql
 SELECT count(*) TotalGames
 FROM chess_games
 
 
 SELECT rated, count(*)RatedGames
 FROM chess_games
 GROUP BY rated
 
  SELECT victory_status, count(*) AS CommonVictoryCount
  FROM chess_games
  GROUP BY victory_status
  ORDER By  CommonVictoryCount DESC
  
  SELECT opening_fullname,count(*)AS CommonOpeningMoves
  FROM chess_games
  GROUP BY opening_fullname
  ORDER BY CommonOpeningMoves DESC
  LIMIT 50

  
  SELECT opening_fullname,white_id,black_id,count(*) AS OpeningTotalCount
  FROM chess_games
  WHERE winner IN ("White","Black") AND victory_status = "Mate"
  GROUP BY opening_fullname,white_id,black_id
  ORDER BY OpeningTotalCount DESC
  LIMIT 50
 
  SELECT round(avg("turns"),2) AS AverageTurns
  FROM chess_games

  
  SELECT round(avg(time_increment),2) AS AverageGameDuration
  FROM chess_games
  
  SELECT max("white_rating") AS MaxWhiteRating, max("black_rating") AS MaxBlackRating
  FROM chess_games

  SELECT winner,count(*)TotalWins
  FROM chess_games
  WHERE victory_status ="Mate"
  GROUP BY winner
  ORDER BY Totalwins
  
  SELECT victory_status,max(turns) AS MaxTurnsVictory, min(Turns) AS MinTurnsVictory,rated 
  FROM chess_games
  WHERE victory_status IN("Mate","Resign","Out of Time")
  GROUP BY victory_status,rated
  ORDER BY rated DESC
  
~~~
  ### Results/Findings
  Results are summerized as following 
  1. there were 20058 games played with an average of 60.47 moves per game
  2. The were only 19.46% games played anonymusly, which is rated false  and the most common victory status was resign with 55.57%
  3. White had more wins compared to black and an average of 14 minutes

### Recommendations 

Based on the analysis 

