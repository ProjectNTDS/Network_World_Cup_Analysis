# Project Wikipedia

DRIVE: 

https://docs.google.com/spreadsheets/d/1M_441_gcpbfUp6pucmgoEl70fSWptNaTiJLhEdhKvhw/edit?usp=sharing

REMARKS : 
Per hour sampling is too hard (according to TA). Limit to per day (feature verctors with 30 entries for 30 days for each node). 

Use API to get the dat (for players):

https://en.wikipedia.org/w/index.php?title=Category:2018_FIFA_World_Cup_players&pagefrom=Layun%2C+Miguel%0AMiguel+Layún#mw-pages 

Also find teams and countries. 


## World Cup project

### Main questions:
1) Network analysis: 
> Can we, based on properties of the nodes, identify the categories in a network made of countries, national teams and players? (should be scale-free). The links are based on the hyperlinks scraped. 

2) Where was the world cup?
> Getting the number of visits on the year on specific sport related categories, can we identify a peak in the popularity of the country matching the world cup? We could normalise that value by the average on a non-world year or a non-world cup part of the year and observe if there's a variation noticable. 

3) Can we identify the date of the matches? Identify the countries that participate at each level?
> Idem for a match on a per day basis centred around the right date. 

> Look at the evolution of number of views. Is there a peak for certain countries matching the match dates? 

> Building a feature graph (connecting players+countries depending on number of visits), can we identify the countries? Could we see the graph evolving in a significant manner when letting it evolve and linking fixed nodes based on the number of visit (above a certain threshold)

4) Identify the players in each team?
> Building a feature graph (connecting players+countries depending on number of visits), can we identify the teams? 

> Using the network (each player is connected to the page of the team), can we cluster football players into the teams that played in the world cup? For exemple, putting a peak on a country should first transmit the heat to the team it is linked to. 

> Slight twist to the network: compute Pearson correlation score between feature vector of each player. High correlation is mostly due to similar behaviour exhibited by the team structure (players of the same team play at the same time and are thus likely to be "wikipedia" on the same time => correlation). Connecting players based on that correlation (threshold), can we, on the resulting network, observe cluster. 

5) Say something about the <b>smoothness</b> of the graph: 
>find date match, observe if there's a peak on the team. Look at the peak on each players. So we limit ourselves to the team, and look at the distribution. Does it link to the team ? Can we spot the players that scored (maybe normalise each player by the average value). Is there a change in smoothness depending on the outcome? (woudln't the less smooth team have more noticeble performances (be them good or bad). 

6) During the match: identify the scoring players and man of the match?
> Should be a peak in number of visits for these nodes.

### Extra questions:
which player is better known than his country?
which players broke into fame following the world cup?

### Use for project:
countries, players, teams 
number of views different timestamps (is an hour reachable?)
world cup schedule for gathering the data
