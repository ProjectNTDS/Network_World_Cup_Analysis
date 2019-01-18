# A Network Analysis of the 2018 FIFA World Cup
In this Readme, you will find in the following order: 
- A link to the report.
- A description of the notebook available on this Github Page.
- A description of the task we set out to answer.
- A description of the data available/used in this project.

# Report link:

https://www.overleaf.com/4566391933wdfgnpfbnpsd

# Description of notebooks:
- Data_Gathering: exposes some of the methods use to gather the data.
- Task_1: expose the analysis of the Hyperlink network (formed by hyperlinks on each Wikipedia Page connecting our nodes). The Louvain method is used here as a first attempt to cluster our graph. Spectral clustering using K-means is also exploited. 
- Task_2: exploit the signal (number of view per days) to perform some basic exploration of our data. Can we identifed when matches happended, which team played? 
- Task_3: from the Hyperlink network, can we cluster nodes into teams exploiting the "heat transmission" approach? Also builds an interesting network based on Pearson correlation between nodes. How clustered is this resulting network? 

A more detailed reasoning behind each task follows.

# THE TASKS
## Why the World Cup?
This playful and light event is an incredible opportunity to extract information from the Wikipedia pages using networks. The first of these is obviously the one formed by the hyperlinks on each Wikipedia Page of interest to this subject: mainly the players, the countries and the national teams. Note that other nodes could have been added such as the stadiums, the referees, .... We however believe that this subsample offer the most interesting opportunities to explore connectivity between these different famlies, clustering aspect of the natural teams and signal analysis. The advantage of such a short time-scaled highly hyped event is that correlation and number of visits will be tightly linked to real-world connections. 

### TASK 0. Get the data:
Note: some of our first ideas needed to sample the number of visits on given Wikipedia pages <b>per hour</b>. The API unfortunately does not offer this possibility.

#### TASK 1. Network analysis:
- Can we, based on properties of the nodes, identify the categories in a network made of countries, national teams and players connected by the hyperlinks (which we shall name <b>hyperlink network</b>? Are leafs players, centre countries, ... ? Is this network scale-free as one would expect? After this exploratory analysis, can we obtain clusters applying the Louvain method ? Let's also not forget  about the opportunities offered by spectral analysis.

#### TASK 2. Finding the matches: 

- Finding which teams played a match on a certain date. Look at the evolution of number of views. Is there a peak for certain countries matching the match dates? 
- Network idea for this: nodes = teams. Links based on number (normalised/fitlered signal?) of visit per month. Finding peaks in the number of views, can we see the countries of the world cup linking each other during the event. 

#### TASK 3. Identifying teams:

- Using the network of hyperlinks (each player is connected to the page of the team), can we cluster football players into the teams that played in the world cup based on a heat signal approach: putting a delta signal on a national team, the heat should first transmit to the team it is linked to.  

- Slight twist to the network: compute Pearson correlation score (or any other metric of simularity) between feature vectors of each player. High correlation is mostly due to similar behaviour exhibited by the team structure (players of the same team play at the same time and are thus likely to be searched on Wikipedia around the same time => correlation). Connecting players based on that correlation (threshold vs selection, since we know that the size of a team is 23), can we, on the resulting network, observe cluster? 

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

# Thank You For Reading !
