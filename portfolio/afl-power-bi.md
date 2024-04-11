---
layout: post
title: "AFL Power BI Report"
date: 2024-04-10
permalink: '/portfolio/afl-power-bi'
---

<p align='justify'>
I created a Power BI report that allows one to investigate a wide range of AFL statistics, from goals scored to bounces, at a season, match and player level.
The .pbix file can be found on my <a href='https://drive.google.com/file/d/17inMSe-Quv3xXVwVQaLnOg7JL_do4Suy/view?usp=sharing'>Google Drive</a>.
Screenshots of the report can be found below.
</p>

Features of the report include: 
    - Navigation buttons on the left-hand side.
    - Disconnected tables used to make side-by-side team comparisons.
    - Interactive buttons using bookmarks.

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/afl-power-bi/report1.jpg"
  style="width:100%"
  >
  <figcaption>
    On the first page, one can view the ladder and a wide range statistics for each team. One can further view the association of this statistic with the performance of the teams.
  </figcaption>
</figure>
</center>

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/afl-power-bi/report2.jpg"
  style="width:100%"
  >
  <figcaption>
  On the second page, one can get detailed statistics for a chosen team.
  The user can also directly compare two chosen teams.
  </figcaption>
</figure>
</center>

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/afl-power-bi/report3.png"
  style="width:100%"
  >
  <figcaption>
  On the third page, the user can view a detailed profile of a selected player.
  </figcaption>
</figure>
</center>

One can select the arrow in the player comparison visual to get a full list of players:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/afl-power-bi/report3-comp.png"
  style="width:100%"
  >
</figure>
</center>

The following is the data model used to make the report:

<center>
<figure>
  <img
  src="https://tomjdove.github.io/TomJDove/assets/afl-power-bi/data model.png"
  style="width:100%"
  >
</figure>
</center>

<p align='justify'>
The data was accessed from the MySQL database created for my <a href='https://tomjdove.github.io/TomJDove/portfolio/afl-sql'>AFL SQL demonstration</a>.
To make the data model better suited for Power BI, I created two new tables, which became the 'Matches' and 'Match Team Score' tables above:
</p>

```sql
CREATE TABLE match_info
SELECT 
    gameID, round, match_date, venue, startTime, attendance, rainfall
FROM game;

CREATE TABLE team_match_outcome 
(
SELECT 
    gameID, 
    homeTeam AS team, 
    homeTeamScore AS score, 
    'Home' as HomeAway
FROM game
)
UNION
(
SELECT 
    gameID, 
    awayTeam AS team, 
    awayTeamScore AS score, 
    'Away' as HomeAway
FROM game
);

```

<p align='justify'>
The problem this solved was that it is inconvenient to analyse individual teams when match data is provided via a pair of teams (the home and away teams). 
Modelling the database in this way separates the match information from the performance of the individual teams, which is more suitable in cases where we, for example, want to find match statistics for a specific team.
</p>

<p align='justify'>
Adding a dimension table containing a list of all the teams further allows us to conveniently filter by individual teams.
The two disconnected team slicer tables, when coupled with the right measures, are used to allow the user to directly two chosen teams.
</p>

