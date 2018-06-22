# The Dataset

The dataset has been generated via exploitation of the **Strava REST API**, the corresponding documentation can be found at (https://strava.github.io/api/)[https://strava.github.io/api/].

We focused on *Segments* resource in order to explore and gather the data of public segments located in North Italy and the Alps along with the corresponding efforts: this data is publicly available once you register on Strava since does not contain sensitive information about platform' users.
In particular, we used these REST endpoint:
*  [`segment explorer`](https://strava.github.io/api/v3/segments/#explore), in order to scan the geographical area of interest for relevant segments;
*  [`list effort`](https://strava.github.io/api/v3/segments/#efforts) so as to collect the comprehensive list of efforts for every segment previously collected via the segment explorer endpoint.
To the end of this preliminary project proposal, we limited the scope of the search to *climb segments* as we feel that hills and mountains can be a well representative sample of road cyclists and mountain bikers' behavior.
Data as been collected using *Python*, exploiting *requests* module and leveraging the flexibility of *Pandas* so as to arrange the dataset in `csv` files.

The resulting files and their corresponding content is described in the following sections.

## Segments 
Segments are paths created by Strava users that can be shared with other members: riders can virtually "compete" on these segments to complete them in the shortest time possible. Segments' data can be found in:

*    [strava-segments.csv](./strava-segments.csv)

The file contains the details of **11058** "climb" segments located in North Italy (covering mostly the Appennines) and in the Alps.
For each segment, a record is provided, showing several features:

*    a *unique integer id* of the segment;
*    the *name* of the segment (e.g. Mont Blanc climb);
*    the *average grade*;
*    the *climb category*, from 1 (easiest) to 5 (the so called "horse categorie");
*    the *total distance* in meters;
*    the *elevation difference* in meters;
*    the data related to *start* and *end latitude* and *longitude*.

## Segment Efforts
The data related to efforts are organized in a series of `csv` files in the [strava-activities.zip](./strava-activities.zip) archive: the total size of the uncompressed data is around 600 MB.
The file contains the details of **5,960,234** different efforts on the **11058** climbs downloaded. 
An *effort* corresponds to a unique attempt at completing a segment by an athlete. The downloaded efforts correspond to rides made mostly in the period from 2009 - January 2018,
though, due to data errors, there are more than *200* activities featuring unlikely years, either way too in the past (1970) or in the future (2019 and further!): this is probably caused by wrong datetime setup on bike computers or smartphones used by athletes 
to upload their activities.

Some or the relevant data for each effort:

*   the anonymized *athlete name* (only first name displayed);
*  	the *start date* in GMT timezone along with the *start date* in *local* timezone;
*  	the *elapsed time* (in seconds), i.e. the total time spent on the segment since start datetime;
*  	the *moving time* (in seconds), i.e. the total time the rider was actually pedalling (this time is usually equal or less than elapsed time);
*  	the *rank*, i.e. the position of the effort on the leaderboard, based on elapsed time, where 1 means KOM/QOM (King of the Mountain/Queen of the Mountain).

## Preprocessing
The only preprocessing performed was to extract year an month information from start datetime of every effort, as well as to parse the data of start and end latitude/longitude of the segments (to facilitate plotting segments on a map).
The resulting file, [activities-parsed.csv.zip](./activities-parsed.csv.zip), contains the combined data of segments and corresponding efforts.