# Project Wikipedia

# Remarks:

- Save your adjacency matrix with an evident name in the sub folder "<b><i>./Data/Adjacencies/</i></b>" and update list next cell.
- Only overwrite these if you're sure of what you're bringing
- Please check your results
- Per hour sampling is too hard (according to TA). Limit to per day (feature verctors with 30 entries for 30 days for each node). 

## Summary of what is available in Data:

### Adjacencies available:
- **adjacency_hyperlinks**: constructed with every category and links based on hyperlinks. **This is directed and it is normal!** If you need it otherwise, symmetrise it and save it in another csv. 
- ...

### With Numbers of Visit

#### Numbers of visit in absolute scale
- All_Nodes_During_WC.csv: a table with every nodes, their categories and the number of visit per day during the World cup itself (the world cup started on 14 June and lasted until 15 July 2018). This starts on the 10th of June and ends on 20th of July (border included). [Remark: for All_Nodes_During_WC.csv, 2 problems occur at the nodes 209 and 572 (Peter Etebo and Ricardo Pereira). Their numbers of visits are set to 0.]

- Countries_Enlarged_During_Year.csv: [for question 2] any countries in any world cup in history. Number of visit per month during the year of the world cup (actually: from 14 November 2017 to (included) 14 November 2018. IMPORTANT REMARK: to help observe the world cup, start of month is set to 14 (since the world cup started the 14th June). The column indicates the month the time started. This is done because otherwise the world cup is cut in two parts.

- Countries_Enlarged_During_Year_centred.csv: same as right above except it starts at the first of the month and goes from Decembre 2017 to Novembre 2018

#### Numbers of visit in Normalised scale
Same files as above but the names end with "_Normalised"

- All_Nodes_During_WC_Normalised.csv: as above but normalised. Last column 'Sum' (index 43) is the total value !!

- Countries_Enlarged_During_Year_Normalised.csv: as above but normalised. Last column 'Sum' (index 14)is the total value !!

### Without Number of Visits
- All_Nodes.csv: each nodes and its category [useful to create a new csv but keep this one clean!]
- Nodes_Linked.csv: each node enters the table with its links in Links and the category of the node in Category(the original one or, equivalently, that in the Nodes column). Use this for the connected network base on hyperlinks (do check that what you obtain is connected!)

#### [UPDATED]

Added file:

- Team_Players.csv : dataset with national team, each players in it, position in the team coded (as in https://en.wikipedia.org/wiki/2018_FIFA_World_Cup_squads) and captain (boolean). <b>Important remark </b>: coding of the names of player DOES NOT ALWAYS MATCH that of the other one (here player name, NOT player page name !). To compare the data, just check the name of the players in this dataframe IS CONTAINED in that of the actual one (subspace obtained may be larger than 1 since several names appear multiple time. Just check that in that subspace, one of the national team match for exemple if you want to check label computed vs true ones). Note also the other is not the same so DO NOT use index comparison. 

### Supplement:
These should not be necessary as they only contain the node and its category in seperated files for each category
Separeted Info:

- players in the 2018 World Cup in All_players.csv
- countries in the 2018 World Cup in All_countries.csv
- teams in the 2018 World Cup in All_National_Teams.csv

And in extra, with more entries than just that World Cup: [modified for question 2 in later]

- any countries in any world cup in Countries_Enlarged.csv


## TASK 0 : get the data
Use API to get the data (for players):

https://en.wikipedia.org/w/index.php?title=Category:2018_FIFA_World_Cup_players&pagefrom=Layun%2C+Miguel%0AMiguel+Layún#mw-pages 

Also find teams and countries in the World Cup. This is done manually

1) need countries not in the world cup. Sample that shit. Maybe every country that ever played in the world cup? 


## World Cup project

Why: network related with an evident hierarchical strucutre (players, teams, country) in one of the most hyped event in the World. 

### Main questions:
#### 1. Network analysis: 
- Can we, based on properties of the nodes, identify the categories in a network made of countries, national teams and players connected by the hyperlinks? Are leafs players, centre countries, ... ? Show network with actual labels coloured (should be scale-free). The links are based on the hyperlinks scraped. 

#### 2. Where was the world cup? Identify the countries that participate at each level?
- Getting the number of visits on the year (2017-2018 on per month basis) on countries, can we identify a peak in the popularity of the country matching the world cup? We could normalise that value by the average on a non-world year or a non-world cup part of the year and observe if there's a variation noticable. Applying high pass filter, it should be standing out of the common fluctuations.

- Network idea for this: nodes = country. Links based on number (normalised/fitlered signal?) of visit per month and a certain threshold. Idea 1: normalise that signal and display an evovling network (one for each month) with nodes fixed. Given a certain threshold, can we see the countries of the world cup linking each other during the event (show it evolving and at that time display the participating countries with colour and check the links connect them. Rapidly eliminated countries may not be linked => conclude). Maybe apply some filter to remove the low frequencies events of each country signal, then normalise and use this as a signal. 

#### 3. Can we identify the date of the matches?
- Idem for a match on a per day basis centred around the right date. - Look at the evolution of number of views. Is there a peak for certain countries matching the match dates? 

- Building a feature graph (nodes =  players+countries  and links depends on number of visits per day and a certain threshold), can we identify the match? Could we see the graph evolving in a significant manner when linking fixed nodes based on the number of visit (above a certain threshold): do players connect naturally when a match has happened? Do we see matches or teams patterns emerging. 

#### 4. Identify the players in each team?

- Using the network of hyperlinks (each player is connected to the page of the team), can we cluster football players into the teams that played in the world cup? For exemple, putting a delta signal on a country should first transmit the heat to the team it is linked to. 

- Slight twist to the network: compute Pearson correlation score (or any other metric of simularity: experiment men/woman!) between feature vector of each player. High correlation is mostly due to similar behaviour exhibited by the team structure (players of the same team play at the same time and are thus likely to be "wikipedia" on the same time => correlation). Connecting players based on that correlation (threshold), can we, on the resulting network, observe cluster. 

#### 5. Say something about the <b>smoothness</b> of the graph (node = players and links arranged to connect the teams): 
- For a given date and a given team, observe signal on the team (each player). Is it smooth or peaky (some players more search). Does it link to the performance of these players and is there a correlation with the result of the match for that team [smoother= lost, peaky = won (high number of good performances giving a lot of search for the associated players)?]. 

[Same but formulated badly : find date match, observe if there's a peak on the team. Look at the peak on each players. So we limit ourselves to the team, and look at the distribution. Does it link to the team ? Can we spot the players that scored (maybe normalise each player by the average value). Is there a change in smoothness depending on the outcome? (woudln't the less smooth team have more noticeble performances (be them good or bad).]

#### 6. Open Question (could be baaaaaad) : During the match: identify the scoring players and man of the match?
- Take a player and show is signal on the month of the world cup. normalise/filter crap and check if any higher peak can be associated to a goal. Can we give a threshold on that signal to conclude that, yes or no, that player scored

### Extra questions (highly useless)
- which player is better known than his country?
- which players broke into fame following the world cup?

### Use for project:
countries, players, teams 
number of views different timestamps (is an hour reachable?)
world cup schedule for gathering the data
