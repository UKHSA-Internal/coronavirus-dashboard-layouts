# coronavirus-dashboard-layouts

The coronavirus-dashboard-layouts GitHub repository contains the YAML files that define the existence, content, structure, appearance and links for all pages displayed on the coronavirus dashboard website.  

**Repository branches**
The [live website](https://coronavirus.data.gov.uk/) sources YAML files from the master branch of this repo.  
The [development website](https://covid19staticdev.azurewebsites.net/developers-guide) sources YAML files from the development branch of this repo.

## Data dictionary
The below defines the objects, parameters and parameter values that have been configured for use within the YAML code.  Further options can be made available but this requires some development to ensure that new features can be correctly interpreted by the websites. 

**Pages**
At the highest level, the website consists of pages, themed by the type of statistic displayed.  Page links are permanently displayed in the static website navigation menu on the left hand side of all pages. With the exception of the UKSummary page, locations can be selected at the page level and data within the page are updated dynamically based on this selection.  Location selection options are defined elsewhere and are beyond the scope of this code repository. 

Each page is defined by a separate YAML file:
* cases.YAML
* deaths.YAML
* healthcare.YAML
* testing.YAML
* UKSummary.YAML

*??Creation of new pages may require development to set up - check ??*

### Main page elements 
Pages display data as **summary**, **headlineNumbers**, or **cards** object types.  

#### summary
summary UK statistics for each page theme - 

Parameters and valid values:
* heading - a list of free text titles defining each page to display a summary object for
* fields - defines each data series to be displayed
    + caption - a list of short text labels for each data series to be displayed 
        - chart
            - value
            - type
            - colour
            - fill
            - rollingAverage
            - display
        - valueItems 
            - label
            - value
            - tooltip


#### headlineNumbers
summary statistics for the latest reporting date displayed at the top of each page

The following parameters can be defined for headlineNumbers:
* caption: a short text label for the headlineNumber.  Free text but suggest 3 word maximum. 1 caption must be defined per headlineNumbers object
* valueItems: defines each of the figures to be displayed under the headlineNumbers object.  See separate definition below
    + label: a short free text label for the valueItem, eg:
        - Daily
        - Cumulative
    + value: the database field name containing the data to be displayed, eg:
        - newCasesByPublishDate
        - cumCasesByPublishDate
        - newCasesBySpecimenDate
        - cumCasesBySpecimenDate
    + tooltip: free text sentence defining the valueItem - reference to {date} will be replaced inline with the latest reporting date for the value.

#### cards
Geographically granular or trend data displayed as charts or tables with associated metadata.

The followig parameters can be defined for cards:
* abstract
* cardType
* downloads
* fullWidth
* heading
* locationAware
* tabs

### Main page element properties

#### valueItems
Defines the data point or series and associated metadata and labelling to be display within an object.
The following parameters can be defined for valueItems:
* label
* tooltip
* value

#### tab
Defines the tabs to be displayed within a card.  The following properties can be defined at the tab level: 
* heading
* tabType
* charttype
* fields

#### locationAware
Controls whether an object is displayed based on the active location selected
The following parameters can be defined for locationAware:
* excluded
    + areaType 
* included
    + areaType

#### abstract
Defines the data presented within a card object in detail.
Free text - suggested maximum length 50 words but can be longer.
Applies to all tabs within the card.  
Use > to display multiple lines of YAML code as single block of wrapped text.

#### fields


### Valid values
Below lists the valid values from parameters referenced above

#### areaType
Defines the active location selected on the web page
* overview
* nation
* region
* England
* NorthernIreland
* Scotland
* Wales

#### barType
Defines how bars are displayed in charts
* group
* overlay
* stack

#### cardType
Defines the format of data presented within a card
* ageSexBreakdown
* chart
* data
* mapStatic
* multiAreaStatic
* scatterStatic
* simpleExternalStatic
* simpleTableStatic

#### clipEnd
Defines the last data point to display for a rollingAverage 
Numeric - usually (n/2)-1 where n is the window value to ensure that incomplete rollingAverages are not displayed

#### colours
Preferred colours, to be used in the ordered series of up to 4 or 3 as outlined below or combined for a series of up to 7

* 0 - pale blue (2)
* 9 - yellow
* 3 - navy blue
* 10 - red

* 6 - grey
* 1 - pale blue (1)
* 4 - pale blue (3)

#### database items
Valid list of database items that can be presented within an object
* newCasesBySpecimenDate
* cumCasesBySpecimenDate
* to be completed...
* etc
* etc

#### display
Defines whether an interactive data series should be selected and displayed in an object by default
* false
* true

#### download
Defines the data available to be downloaded
Valid values include any database data items (see separate entry under database items)

#### fill
Defines whether the area under a line chart in an object should be shaded or not
* false
* true

#### fullWidth
Defines whether an object should fit to the full page width or allow other objects alongside
* false
* true

#### heading
Short text labels
* about
* cumulative
* daily
* data

#### label
Defines the label that will be associated with a figure or object
Short free text string

#### params
Defines the data series to be displayed, overriding the selected location within a page
The following parameters must be defined in each case
* key - the selected parameter to override (valid values: areaType)
* sign - the operator to apply to the filter (valid values: =)
* value - the key value to apply to the filter (valid values: see separate entry under areaType)

#### rollingAverage
Defines whether to include a 7-day rolling average in a chart or data object
Can also specify window and clipEnd parameters
* false
* true

#### tabType
* chart
* metadata
* table

#### tooltip
Defines the hover text that will displayed for an object
Free text sentence 
Depending on usage, a {date} parameter may be included for inline insertion of the latest reporting date:
* cards - {date} unavailable
* headlineNumbers - {date} available
* summary - {date} available

#### type

* bar
* date
* line
* numeric
* radio
* string


#### value
Defines which data point or data series will be displayed in an object
Valid values include any database data items (see separate entry under database items)

#### window
Defines the time period to group for the rollingAverage parameter
Numeric - usually 7 for a rolling weekly data series


