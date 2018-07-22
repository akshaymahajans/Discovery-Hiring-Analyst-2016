# Data Analysis Task

Task description and data for candidates applying to be a Data Analyst in the DSBA team at Branch.

## Background

Branch's core platform keeps logs of activities made by *Persona* ID's -- a persona ID is a unique identifier for a specific iPhone's activity of app usage and mobile link clicks. Specifically, DSBA is interested in:

- *open rate*: the proportion of sessions where the persona opened an app
- *campaign click-to-install rate* - the proportion of marketing campaign clicks where the persona ultimately installed the app

and other metrics outside the scope of this task. Persona derives its data from Javascript cookies, which send information about the user's device and web browser to our servers when a persona engages with a Branch link. In this task, you will analyze a subset of our Persona data. 

## Task

You must create a **reproducible report**\* answering the following questions:

1. What is our daily overall open rate? How does it vary between app verticals?
2. Which verticals do personas engage (click licks) for most? How does it change day-to-day?
3. What is the average campaign click to install rate? How does it vary day-by-day? By vertical?
4. Let *persona duration* be approximately the time between the first event (click or open) for a persona and the last event for a persona. Choose a variable from the dataset and describe its relationship to persona duration. Visualize the relationship.
5. Summarize your findings in an *executive summary*.

\* Given dependencies and other instructions, we should be able to re-run your source code with the dataset in the same directory and obtain the same results and figures. Popular formats for this include RMarkdown and Jupyter Notebook (formerly IPython).

**Note**: if you submit your report as a Jupyter/IPython notebook on Greenhouse, please upload a copy to GitHub and include the link when you submit it on Greenhouse.

## Data

The dataset comes from a [tracking schema](https://meta.wikimedia.org/wiki/Schema:TestSearchSatisfaction2) that we use for assessing user satisfaction. Desktop users are randomly sampled to be anonymously tracked by this schema which uses a "I'm alive" pinging system that we can use to estimate how long our users stay on the pages they visit. The dataset contains just a little more than a week of EL data.

| Column          | Value   | Description                                                                       |
|:----------------|:--------|:----------------------------------------------------------------------------------|
| uuid            | string  | Universally unique identifier (UUID) for backend event handling.                  |
| timestamp       | integer | The date and time (UTC) of the event, formatted as YYYYMMDDhhmmss.                |
| session_id      | string  | A unique ID identifying individual sessions.                                      |
| group           | string  | A label ("a" or "b").                                     |
| action          | string  | Identifies in which the event was created. See below.                             |
| checkin         | integer | How many seconds the page has been open for.                                      |
| page_id         | string  | A unique identifier for correlating page visits and check-ins.                    |
| n_results       | integer | Number of hits returned to the user. Only shown for searchResultPage events.      |
| result_position | integer | The position of the visited page's link on the search engine results page (SERP). |

The following are possible values for an event's action field:

- **searchResultPage**: when a new search is performed and the user is shown a SERP.
- **visitPage**: when the user clicks a link in the results.
- **checkin**: when the user has remained on the page for a pre-specified amount of time.

### Example Session

|uuid                             |      timestamp|session_id       |group |action           | checkin|page_id          | n_results| result_position|
|:--------------------------------|:--------------|:----------------|:-----|:----------------|-------:|:----------------|---------:|---------------:|
|4f699f344515554a9371fe4ecb5b9ebc | 20160305195246|001e61b5477f5efc |b     |searchResultPage |      NA|1b341d0ab80eb77e |         7|              NA|
|759d1dc9966353c2a36846a61125f286 | 20160305195302|001e61b5477f5efc |b     |visitPage        |      NA|5a6a1f75124cbf03 |        NA|               1|
|77efd5a00a5053c4a713fbe5a48dbac4 | 20160305195312|001e61b5477f5efc |b     |checkin          |      10|5a6a1f75124cbf03 |        NA|               1|
|42420284ad895ec4bcb1f000b949dd5e | 20160305195322|001e61b5477f5efc |b     |checkin          |      20|5a6a1f75124cbf03 |        NA|               1|
|8ffd82c27a355a56882b5860993bd308 | 20160305195332|001e61b5477f5efc |b     |checkin          |      30|5a6a1f75124cbf03 |        NA|               1|
|2988d11968b25b29add3a851bec2fe02 | 20160305195342|001e61b5477f5efc |b     |checkin          |      40|5a6a1f75124cbf03 |        NA|               1|

This user's search query returned 7 results, they clicked on the first result, and stayed on the page between 40 and 50 seconds. (The next check-in would have happened at 50s.)
