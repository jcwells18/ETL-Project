# ETL-Project
Github Repositories:
Julie Wells - https://github.com/jcwells18/ETL-Project
Junette Lee - https://github.com/junettel/ETL-project
Amusa Adebayo - https://github.com/aadeba5/ETL-PROJECT 


Data Sources:
Streaming Data - Movies on Netflix, Prime Video, Hulu and Disney+
IMBb Data - IMDb movies extensive dataset


Extract:
Downloaded data CSVs from Kaggle and loaded into Python to use Pandas for transformation and cleanup
Streaming csv: provides comprehensive list of movies on streaming platforms with film information
IMDB movies csv: includes additional columns (movie descriptions, IMDB title IDs)
IMDB titles csv: provides mapping of IMDB title IDs and IMDB name IDs of cast members
IMDB names csv: includes information on movie cast and crew members along with an IMDB name ID

Transform (Data Cleanup & Analysis):
Steps to complete:
Cleaning:
Dropping unnecessary columns from each source - streaming csv and movies csv had overlapping/repetitive columns, so we mainly dropped columns from movies csv
Cleaning column names to omit spaces so information smoothly flows to pgAdmin
Harmonizing rating metrics (Rotten Tomatoes, %) in MoviesOnStreaming and IMDb movies rating (as metascore)
Stripping ‘%’ sign from Rotten Tomatoes rating so it may be formatted as a float rather than object
Split out name of most recent spouse from 'spouses_string' in names csv
Split out place of birth data string from names csv into separate columns
Split out place of death data string from names csv into separate columns

Joining: 
Joined/merged the streaming and imdb movies data sets by title and year
By joining streaming csv with movies csv, we are able to add imdb_name_id

Filtering: 
Filtered out all movies not currently on one of the streaming platforms through an inner join on the streaming csv
Inner join also filters out movies on streaming platforms missing IMDb data or with contradicting title/year information so only exact matches are included

Aggregating: 
Average IMDb and Rotten Tomatoes ratings calculated after Load step
Can be done either in pgAmin by SQL query or by using Python and SQLalchemy
Summed streaming platforms for number of platforms per movie

Load:
Loaded data tables into relational database, pgAdmin (postgres)
Final tables loaded to database:
Movies - streaming platform movies with unique imdb_title_id
Actors/Names - actor/personnel information with unique imdb_name_id
Titles - provides mapping between Movies and Actors Tables using imdb_title_id and imdb_name_id
Reasoning: We chose these tables to be able to utilize the imdb_title_id and imdb_name_id mappings to connect movies streamed with the appropriate actors/directors
We chose a relational database because the imdb_title_id  and imdb_name_id, unique alphanumeric identifiers for each movie or actor/actress, connect the three database tables and broaden the search and query possibilities while keeping the tables more focused


