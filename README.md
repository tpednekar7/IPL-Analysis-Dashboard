                        🏏 IPL Analysis Dashboard — Power BI
An interactive Power BI dashboard analyzing Indian Premier League (IPL) data from 2008 to 2022, covering batting, bowling, match results, and team performance across all seasons.

📸 Dashboard Preview

(Add your dashboard screenshot here)


📁 Dataset
Two tables used:
1. ipl_ball_by_ball_2008_2022 — Ball-by-ball delivery data
ColumnDescriptionidMatch ID (Primary Key, links to matches table)batter / bowlerPlayer namesbatsman_runRuns scored off the batiswicket_delivery1 = wicket, 0 = no wicketextra_type / extras_runWide, legbye, no-ball etc.total_runTotal runs on that deliverybatting_teamTeam currently batting
2. ipl_matches_2008_2022 — Match-level data
ColumnDescriptionidMatch ID (Primary Key)seasonIPL season yearteam1 / team2Competing teamswinning_teamMatch winnerwon_byWickets / Runs / SuperOvertoss_winner / toss_decisionToss resultvenue / cityMatch locationplayer_of_matchBest performer

🎛️ Filters
SlicerFieldDescription
🗓️ Select SeasonseasonFilters entire dashboard by IPL year (2008–2022)
🏏 Select BatsmanbatterFilters batting stats section
🎳 Select BowlerbowlerFilters bowling stats section

📊 KPI Cards
KPIDescription
🏆 Title WinnerWinning team for selected season
🟠 Orange CapBatsman with highest runs in selected season
🟣 Purple CapBowler with highest wickets in selected season
6️⃣ Tournament 6sTotal sixes hit across selected season
4️⃣ Tournament 4sTotal fours hit across selected season

📈 Visuals
🏏 IPL Batting Stats
Stats for the selected batsman in the selected season:

Total Runs
Total 6s
Total 4s
Strike Rate

🎳 IPL Bowling Stats
Stats for the selected bowler in the selected season:

Total Wickets
Economy Rate
Bowling Average
Bowling Strike Rate

🍩 Matches Won Based on Toss Decision
Donut chart showing proportion of matches won by teams that chose to field vs bat after winning the toss.
🍩 Matches Won by Result Type
Donut chart breaking down wins by Wickets, Runs, or Super Over.
📊 Total Wins by Team for Season
Clustered bar chart showing total match wins per team for the selected season.
📊 Matches Win by Venue
Clustered bar chart with:

Y-axis → Venue
X-axis → Count of matches (count of id)
Legend → Won by (NoResults / Runs / SuperOver / Wickets)


🔑 Key DAX Measures
dax-- Purple Cap: Top wicket taker
bowlers wickets = 
SUMX(ipl_ball_by_ball_2008_2022, ipl_ball_by_ball_2008_2022[iswicket_delivery])

-- Orange Cap: Top run scorer  
Batter runs = SUM(ipl_ball_by_ball_2008_2022[batsman_run])

-- Strike Rate
Strike Rate = DIVIDE(SUM(ipl_ball_by_ball_2008_2022[batsman_run]), COUNT(ipl_ball_by_ball_2008_2022[ball_number])) * 100

-- Economy Rate
Economy = DIVIDE(SUM(ipl_ball_by_ball_2008_2022[total_run]), COUNT(ipl_ball_by_ball_2008_2022[ball_number])) * 6

⚠️ For Top N filters (Orange Cap / Purple Cap), always use the numeric measure in the "By value" field, not the display measure with text concatenated.


🛠️ Tools Used

Power BI Desktop — Dashboard, DAX, visuals
Power Query (M) — Data cleaning, type corrections
DAX — KPIs, aggregations, Top N filtering
Two-table data model — Ball-by-ball joined to match-level via id


🗂️ Data Model
ipl_matches_2008_2022 (id) ──── (id) ipl_ball_by_ball_2008_2022
         [One]                           [Many]

Data covers IPL seasons 2008 – 2022 | 🏟️ 74,000+ deliveries
