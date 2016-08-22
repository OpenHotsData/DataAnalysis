### Proposal for data to be available on OpenHotsData

Document version: 1.0

Authors: Alexander Kunze

#### Introduction

For better categorization and perhaps placement on the website, the data that we
calculate from the replays falls into four categories:

- _Global_ - statistics that span all players, all games, all talents, all heroes.

- _Player_ - statistics that apply to one particular player only.

- _Hero_ - statistics that apply to a single hero.

- _Talents_ - statistics that apply to single talents or talent builds.

- _Maps_ - Statistics that apply to a single map

In addition, we distinguish between the following calculation types of data:

- _Direct_ - Data that is immediately available from the game itself and merely
  needs to be summed up to display on the web page.

- _Calculated_ - Data that is in some way processed. This includes averages,
  confidence intervals and percentages.

- _Historicized_ - Data that can be plotted against time. This includes most data, but some
  exceptions exist and are mentioned below.
  
- _Sub levels_ - Levels for which this layer can be further broken down. For example:
  Heroes have their own data (e.g. how many kills are achieved on average with this
  hero), but also data specific to certain maps (e.g. allowing sorting of all maps
  according to win rate for this particular hero). 
  Likewise, maps in return have data for all heroes (allowing the sorting of win
  rates for all heroes).

#### Data breakdown

- Global
    - Direct
        - Players recorded
        - Active players (defined as players who appear in any replay during the
          last month)
        - Replays uploaded
  
    - Calculated
        - Standard set of averages per game for an average player

    - Historicized
        - All totals and averages

    - Sub levels
        - Players
        - Heroes
        - Maps

- Players
    - Direct
        - Games played
        - Time played
        - Combined hero level

    - Calculated
        - MMR Information
        - Win rate
        - Standard set of averages per game for this player

    - Historicized
        - All totals

    - Sub levels
        - Heroes
        - Maps

- Heroes
    - Direct
        - Games banned
        - Games played
        - Games won

    - Calculated
        - Popularity
        - Win rate
        - Win rate delta w.r.t. specified time period (adjusted by player)
        - Standard set of averages per game for this hero

    - Historicized
        - All totals except win rate delta
        
    - Sub levels
        - Talents
        - Maps

- Maps
    - Direct
      - Objectives (i.e.: How many gems collected, lost and turned in on Spider
        queen map)
    - Calculated
        - Standard set of averages per game for this map
    - Historicized
        - All data
    - Sub levels
        - Heroes


- Talents / Talent builds
    - Direct
        - Games played
        - Games won
    - Calculated
        - Popularity
        - Win rate -> Should be calculated as follows: If the hero is played
          1000 times in the period, and when taking talent X, 500 games resulted
          in a win, the win% is 50% for that talent. Do independently for every
          talent
        - Standard set of averages per game for this talent / build
    - Historicized
      - All data
     

#### Standard set of averages
 
A variety of data that can be summed up and then averages can be employed at
various levels: For players, for talent builds or for heroes. This "standard
set" is:

- Kills - Called "SoloKill" in the replay
- Assists
- Takedowns (Assists + Kills)
- Deaths
- Hero Damage
- Siege Damage
- Ability Damage
- Auto Attack Damage
- Healing performed
- Self Healing (Note: Careful, the replays lump healing and self healing
  together!)
- Average game length
- APM
- Experience Contribution
- Time CCed enemy heroes
- Time spent dead
- Feed amount - Experience given to the enemy team by dying
- Takedowns / Deaths
- Damage taken / Death
- Experience Contribution / Feed Amount


#### Confidence intervals

Every calculated statistic should include either the standard deviation or the
confidence interval.

For calculated averages, such as those in the standard set, always give the
standard deviation. Example: 30'000 +/- 6'000

For percentages, give the standard 95% confidence interval. Example: Win% = 56%
+/- 17% Note: It is also possible to give the confidence interval differently,
such as in the above example: 39-73%. This may be given in parentheses nearby,
such as: 56% +/- 17% (39%,73%) Whether such a notation is useful or desirable
for the player remains to be seen.

Note that for small sample sizes (typically N < 30), the statistics become so
poor as to give no reasonable data.


#### History data and graphs

An additional and useful feature are graphs. These graphs show data over time,
and can be used for the duration of a single game or can show averaged data over
several games for a specific time period (say for a month) and for a specified
time resolution (which specifies over what time period we average, say minutes
for a game or a day for multiple games).

All the data mentioned under historicized can be implemented as a graph,
although some data is only useful as data over several days, such as an MMR
graph.

Graphs, if implemented, should ideally be zoomable, or at least restrictable to
a certain time period with a calendar. The graphs should show the time as x axis
and whatever metric is being measured as y axis.

In addition, the resolution should also be choosable, either automatically
(through the zoom level) or by the player (average data over one day, one week,
two weeks? etc.) For now, the resolution should be kept at a minimum of days
(there is no point in historicizing data by the hour) and a maximum of years.
For game time data, the maximum resolution should probably be ~10 seconds and no
less. Averaging over individual seconds would yield very spiky graphs that are not 
useful.

In addition, it would be great if the graph had colored bars at the bottom below
the x axis, corresponding to the different version lengths, giving the player
the option to see at which point in time which game version was active. A
further feature (discussed below) would be to restrict the data to only (a)
specific version(s).
An additional bar could designate the current season.


#### Additional ideas

- _Sub roles_: Split-up of player statistics according to hero sub roles
- _Cross-correlations_: Data between players and heroes.  Meaning: What are the
  statistics (win rate and standard set) when playing against or with player /
  hero X. Can be extended towards the maximum.  I.e.: What are the statistics
  for Tassadar, assuming he plays with E.T.C, Li Ming, Zeratul and Nova?
- _Ability vs AA damage_: A very useful addition would be the splitting up of
  ability damage vs autoattack damage. This would be invaluable in choosing, for
  example, whether to use a spell shield talent. It would allow calculation for
  example: How much of a reduction do we get on average by using this talent
  compared to another one?
- _Statistics warning_: Warning to players when statistics are unreliable
  Although players should be able to read the confidence intervals themselves,
  it may be useful to add a warning sign (such as a red exclamation mark), if
  there are too few statistics to give any useful guidance. Example: Only 20
  games played.
- _Versioning_: There should be an option for players to only look at data from
  a specific version. That way, no matter what time range a player selects, only
  data from the specified version is shown. "Latest version" should be its own
  option and should always be on top for easy accessibility.  An extension to
  this would be to restrict the data only to a particular season.
- _Effective damage_: Damage that went towards an actual hero kill. For example:
  Simply shooting Chen with Valla while he keeps drinking would give very high
  hero damage, but the damage is completely wasted and useless. Ideally, we can
  record what went towards a hero kill. We can get at that info because the game
  records it (death recap information), so reaching this information and using
  it would be very useful.


#### Further notes

Effective damage, damage that was done in death recap, who did how much damage!
