# Project Wikipedia

REMARKS : 
Per hour sampling is too hard (according to TA). Limit to per day (feature verctors with 30 entries for 30 days for each node). 
Use API to get the data: 
https://en.wikipedia.org/w/index.php?title=Category:2018_FIFA_World_Cup_players&pagefrom=Layun%2C+Miguel%0AMiguel+Layún#mw-pages for players
Also find teams and countries. 


## World Cup project

### Main questions:
1) Network analysis.: Can we, based on properties of the nodes, identify the categories in a network made of countries, national teams and players?  (should be scale-free)


2) Where was the world cup?
> Getting the number of visits on year on specific sport related categories, can we identify a peak matching the world cup? 

3) Can we identify the date/time of the match?
> Idem for a match on a per day basis centred around the right date.  


4) Identify the countries that participate at each level?
> Look at the evolution of number of views. Is there a peak for certain countries matching the match dates? 
> Building a feature graph (connecting players+countries depending on number of visits), can we identify the countries? 

5) Identify the players in each team?
> Building a feature graph (connecting players+countries depending on number of visits), can we identify the teams?
> Using the network (each player is connected to the page of the team), can we cluster football players into the teams that played in the world cup? For exemple, putting a peak on a country should first transmit the heat to the team it is linked to. 
> Slight twist to the network: compute Pearson correlation score between feature vector of each player. High correlation is mostly due to similar behaviour exhibited by the team structure. Connecting players based on that correlation (threshold), can we, on the resulting network, observe cluster. 

6) During the match: identify the scoring players and man of the match?
> Should be a peak in number of visits for these nodes.

### Extra questions:
which player is better known than his country?
which players broke into fame following the world cup?

### Use for project:
countries, players, teams 
number of views different timestamps (is an hour reachable?)
world cup schedule for gathering the data
