# nhl_pbp_strength_data

Read my [blog on Power Play Efficiency](https://www.k2nflstats.com/#/blogs/power_play_efficiency), using data gathered from this notebook.

This scraper is a Jupyter Notebook and uses data from HockeyR: https://github.com/danmorse314/hockeyR-data

The requirements for this Notebook are Python 3.10.

## Inspiration
Why create an NHL pbp game managing system? I was curious about diving into power play (PP) efficiency as there is a glaring problem with the traditional percentage metric (PP goals/total PP opportunities): the equality of short and long power plays. On one hand, a team can be short-changed for converting short PPs while other teams aren't truly punished for squandering long PPs.<br />

With inspiration from a [Medium Article on Power Play Efficiency](https://medium.com/second-look/nhl-should-change-how-we-calculate-power-play-efficiency-8b8b9ea93883), I wanted to investigate this.<br /><br />

Unfortunately, the specific data in the HockeyR repo I needed wasn't granular or consistent enough for my inquiries, so I needed to create my own system. Essentially a game managing system which looks at games on a play-by-play basis and uses the protocols outlined in the NHL Rulebook to manage the penalties incurred during a game (spoiler: it's a bit complex).

## Methodology
I first scrubbed the NHL Rulebook to understand when power plays occur, for how long, and their terminating conditions. After getting a good understanding, I began creating the Game object which essentially does the job of a Penalty Clock Manager (a real job at each hockey game), along with some other metric tracking capabilities.

I'll post a write-up for anyone interested in the nitty gritty of the system, but it really is complex--much to the chagrin of NHL players. 

## Functions

<code>scrape_pbp()</code><br />
This main function scans an entire season (or more) of plays and keeps track of the TOI (time on ice), GF (goals for), and GA (goals against) for each team at each strength.

<code>collect_data()</code><br />
This function invokes <code>scrape_pbp()</code> and creates a Dataframe, which is then output to a csv file. After scraping the specified years, this breaks down the data by team-seasons and provides TOI, GF, and GA for each possible strength.<br />

Arguments:<br />
<code>first_year</code>: first year to scrape, i.e. 16 for 2016, 17 = 2017, etc.
<code>last_year</code>: last year to scrape. Same format as first_year.
<code>playoffs</code>: boolean; if True, scrapes playoff games; else, regular season games only.

## Debugging Functions
<code>scrape_pbp_debug()</code>
Used to look at specific games in the pbp in debug mode to test functionality. Make sure to read the comments around that function for instructions.

<code>print_coincidental_penalties()</code>
Used to gather the different combinations of batches of penalties assessed at the same stoppage. This is related to coincidental penalties as well as determining power play type and length.


