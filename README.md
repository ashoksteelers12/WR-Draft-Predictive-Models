<p align="center">
  <a href="https://en.wikipedia.org/wiki/DK_Metcalf"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/50/DK_Metcalf_%2850744645202%29.jpg/330px-DK_Metcalf_%2850744645202%29.jpg" alt="PHP Logo" height="200" width="300"></a>
</p>

# Predictive Models For WRs In The NFL Draft

[![forthebadge](https://forthebadge.com/images/badges/made-with-python.svg)](http://forthebadge.com)

A set of predictive models to help determine accurate ways for predicting the selected round for WRs in the NFL Draft by utilizing a combination of TDA and ML techniques, such as k-means clustering, persistent homology, and random forest classifier. The project additionally analyses previous drafts with a focus on WRs from Power Five conferences in the 2018, 2019, and 2020 NFL Drafts, who were also invited to the NFL Combine. 

## Table of Contents

- [About](#about)
  - [Scope](#scope)
  - [Layout](#layout)
- [Data Collection](#data-collection)
- [Methods](#methods)
- [Usage](#usage)
- [References](#references)

## About

### Scope

The project does NOT: 
- Include all positions and all WR prospects
- Include drafts other than 2018, 2019, and 2020
- Take into account trades
- Take into account anything related to the 32 NFL teams
- Take into account all WR statistics
- Include PHs for thresholds greater than 5
- Simulate picks

### Layout

The following folders contain: 
- Game-Stats-2018: Contains CSV files with game-by-game statistics for each player during their final college year
- Game-Stats-2019: Contains CSV files with game-by-game statistics for each player during their final college year
- Game-Stats-2020: Contains CSV files with game-by-game statistics for each player during their final college year

## Data Collection

Data was manually collected from Sports Reference and NFL's site. The game-by-game statistics were taken from Sports Reference, while the prospect grades and draft results were taken from NFL's draft tracker. Data was both stored in CSV files and directly pasted into the code (Manual-Data-Collection.ipynb). 

Each prospects had a set of parameters (some manually collected and directly pasted, while other calculated in the program): 
- Name (Integer): First and last name of the player
- Conference (String/Integer): Conference the player played in (Started off as string, then converted to integer for predictive model)
- College (String): College the player is from
- Year (Integer): Draft year (2018 or 2019 or 2020)
- Grade (Float): Draft grade assigned by NFL's draft experts
- Round (Integer): Round # selected in (1-7 with 0 as undrafted)
- Class (Integer): Class of player (Junior is 3, Senior is 4, r-Junior is 4, r-Senior is 5, etc.)
- H0, H1, H2 (Integer): Persistent homologies calculated for game-by-game statistics
- CG (Integer): Clusters of conference and grade
- GH (Integer): Clusters of grade and H0 

## Methods

PERSISTENT HOMOLOGY: Persistence diagrams were displayed for each WR by plotting birth time against death time. Since persistence is basically the vertical distance from a corresponding point to the diagonal of the  diagram, which is the line signifying birth time is equal to death time, these diagrams were used  to figure out the consistency of a WR’s performance in his last year in college. The factors taken  into account to determine a consistent performance were receptions, yards, and touchdowns. The  goal was to see how much of a factor this played into which round a WR would be taken in. The  program has a threshold of 999 but the points on the graph are only counted up to a threshold of 5  as the scale of the diagrams were only plotted till 5 on both the vertical and horizontal axes. The  scale was limited for identifying the number of close values to incorporate the count in the predictive models. The infinity value was first accidently included into the count, but was kept after determining it would not affect the outcome as every player’s homology count would increase by 1.

K-MEANS CLUSTERING: Clustering is beneficial to determine which values are more “next” to each other compared to  others. The clustering involved in the project was primarily used to see how clustering by and without homologies helps in improving accuracy. It was also used to identify which values were  influential in determining the drafted round. The program uses k-means clustering because of its simple implementation. It may not be the best clustering method for this particular project, but  using it will help determine how effective k-means can be in predictive models. Of course, this depends on what is being clustered.

Clustering done: 
- Conference and grades
- Grades and H0

RANDOM FOREST: Since the primary purpose of this project was to determine the effects of clustering and persistent homology, the type of ML algorithm will not matter. It is important to note that the type of ML algorithm used  will affect the accuracy of the model, but in terms of this project, the goal may be accomplished  with any algorithm. Random forest classifier was preferred over the regressor because it involves  the classification of conferences and rounds. The random forest was done multiple times for  various parameters to see the varying accuracy. The goal of each model is to predict the right round, so the round values were the “y” of the dataset.

Random forest done with “X” as:
- Grades
- Persistent homologies (H0, H1, H2)
- Cluster of conference and grades
- Cluster of grades and H0
- Persistent homologies and cluster of grades and H0
- Everything except persistent homologies and both clusters
- Everything
- Grades and cluster of conference and grades
- Grades and cluster of conference and H0
- Grades and class

## Usage

The project must be run in the following order of files: 
1. Manual-Data-Collection.ipynb
2. Persistent-Homology-Analysis.ipynb
3. NFL-Draft-2018.ipynb
4. NFL-Draft-2019.ipynb
5. NFL-Draft-2020.ipynb
6. Clustering-Analysis.ipynb
7. Predictive-Model.ipynb

## References

[Sports Reference](https://www.sports-reference.com/)

[NFL](https://www.nfl.com/)
