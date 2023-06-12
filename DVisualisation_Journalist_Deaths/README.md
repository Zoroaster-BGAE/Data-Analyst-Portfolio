# Data Visualization MSc Assignment #
      This repository contains the code and data for my MSc assignment on data visualization. 
      The purpose of this project is to create an interactive map 
      that showcases the least friendly regimes on free speech around the world. 
      The map utilizes a dataset called "The Lost Journalists Dataset," 
      which consists of 1879 reported missing cases of journalists from 1992 to 2017.

## Dataset ##

The "Lost Journalists Dataset" includes the following columns:

    * Date of the incident
    * Name of the victim
    * Sexual orientation of the victim (if confirmed)
    * Country where the incident took place
    * Organization
    * Nationality
    * Medium of reach
    * Job
    * Topic coverage
    * Indigenousy
    * Type of group associated with the incident
    * Type of death
    * Impunity of the propagating member (Yes, No, Partial)
    * Captivity of the victim (True or False)
    * Reported threats against the victim (True or False)
    * Reported torture conducted against the victim (True or False)

Additionally, the dataset incorporates information retrieved from the Plotly country codes library, including three-letter country codes. The data is publicly available on Kaggle and does not violate any copyright restrictions. To ensure privacy and ethical considerations, the dataset does not contain specific names of the victims.

## Project Description ##

The main objective of this data visualization project is to create an interactive map that highlights the regimes worldwide with the least favorable conditions for free speech. The visualization aims to present both qualitative and aggregate data, shedding light on the reasons behind the majority of reported cases and their correlation with historical events.

The resulting map will be used in a BBC associates meeting where topics such as fair pay rates for journalists covering stories in dangerous countries will be discussed. The visualizations need to be interactive as they encompass three distinct dimensions: latitude, longitude, and time. Users should be able to explore the map and retrieve essential information about the majority of cases by hovering over a specific country and time period. This information can then be correlated with news from that year, setting the tone for future predictions on similar events' coverage.

The project falls under the "Exploratory" and "Feeling" categories in the purpose map. It provides users with the opportunity to gain their own insights by interacting with the data and other available information. While the visualization aims to enhance comprehension, it also evokes emotional responses, which are significant considering the intended audience of journalists themselves.

## Data Processing ##

Upon downloading the data, certain issues were addressed. Column and row names were reviewed and modified as needed. Irrelevant columns, such as those with NA values or containing uninformative names (e.g., x1, x2, etc.), were ignored. Additionally, column names were standardized, and binary variables were transformed into 0 and 1 for ease of use.

The original date format provided detailed information that would result in a cluttered time axis. To address this, the date column was transformed to include only the years. While some data was lost due to descriptive date entries (e.g., "Somewhere between May 3rd and May 9th"), the loss was minimal (less than 100 entries). The dataset now covers the years 1992 to 2008.

To ensure compatibility with the Plotly library's mapping functionality, a library containing country names and their associated ISO-3 codes was utilized. A left-join operation was performed to merge the two tables, and manual adjustments were made to ensure matching country names. Controversial entries, such as "Israel and the Occupied Palestinian Territory," were simplified to "Israel" for the purposes of this investigation, without taking a stance on the conflict. The dataset also accounted for border changes that occurred between 1992 and 2008, renaming

## Execution ##

To execute this project either download and open the html file or create a new project in your R studio and parse in the code and the CSV's as well. Run the code until your map object is displayed properly (all interactive features work as planned).
