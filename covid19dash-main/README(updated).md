First cell:

This cell of code sets up the imports I am using, global variables, and
the configurations necessary for fetching, processing and visualising
the covid 19 and other resp virus data. This is done by setting out the
file path for the timeseries file I use to make the timeseries graph, a
dictionary containing respiratory virus APIs, and my lineage data API
along with the output file where Im storing the data. The global
variables are just 3 dataframes to hold the time series, lineage, and
combined resp virus positivity rate data. The output widgets are pretty
self explanatory - just widgets to display the plots and outputs for all
the data, and an extra widget to display debug logs during the API
requests.

Second cell:

This cell contains all the functions needed to handle the covid time
series data. Wrangle data reads and processes the data from a json file,
converts it to a pandas dataframe, normalizes it, converts the date
column to datetime, and then plots the plots it on a timeseries graph.
Additionally, if there\'s no data in the frame, or the columns are
structured incorrectly, it returns an error message (no data available
to plot). The plotting function plots, and the refresh function
refreshes the plot based upon metrics selected by user from a dropdown
menu.

Third cell:

This cell\'s functions handle the lineage data. This includes fetching,
saving, processing and plotting the data. It fetches data from the API
with a while loop that works so long as more pages from the url exist,
combines it all into a dataframe and handles previous errors I fixed
that happened when data fetching failed. It then converts and saves the
lineage data to a json file. It then cleans the data by filtering by
metric and changing date to datetime. It then plots it on a graph, and
the final function combines all of this to be done by a button the user
presses.

Fourth cell:

This cell fetches, processes and plots a timeseries graph for 5
different respiratory viruses (Adenovirus, hMPV, influenza, rhinovirus
and RSV). The graph is for positive test rates. It fetches the pages
with a delay as I kept getting timed out when I didn\'t use a delay,
thus failing to generate results. It does this by iterating through the
pages using the next URL, packages it and returns it in a dataframe
containing data for each virus with an added column for the virus name
(fetch_all_pages). It then iterates through the API dictionary of URLs
for the different viruses, using the fetch_all_pages function to receive
data for each virus and combines each individual dataframe into a
consolidated dataframe (fetch_and_combine_data). It outputs error
messages when data cannot be received and a success message when all
data is fetched. It then cleans the data, selecting only relevant
columns, and renames metric_value to PositivityRate for greater clarity
for the user. All of this is done when the user clicks the
\"rip_data_from_apis\" button.

**IMPORTANT KET NOTE PLEASE READ BEFORE TRYING TO USE THE BUTTON:** This
process loops through (I think it was) 5164 pages worth of data. With
the 200ms delays, this takes around 15 to 20 minutes, and the risk of
certain data being lost totimeouts isnt entirely mitigated (though the
grand majority of the data will be receieved and plotted). Just bear in
mind this process will take a long while. You will know it works as when
one virus\' pages has been fetched, it will give a message moving onto
the next one. Please please please bear this in mind when using.

Fifth cell:

This cell just defines the interactive widgets so that the user can
select options and trigger the functions for dealing with the data.
There\'s a dropdown menu for the timeseries metrics, the rip from
lineage button and the rip from respiratory button.

Sixth cell:  
  
This cell just clears existing outputs and displays the buttons. This is
so a clean display can be created for updates and so that the user has
something to interact with.
