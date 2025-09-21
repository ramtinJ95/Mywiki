# Data Strategy

## Discuss with company leadership
We need to treat data as a first class citizen. Meaning we need to consciously
define how we want data to work. Define how you want to look at at the business
and then build the environment that delivers that at the cadence and quality the
business needs. The data org needs to know how the organization takes
decisions. The data org needs to be clear on how what they produce is used,
where it is used and what are the goals. 

Then after that discussion the leadership together with the data lead need to
come to an agreement on what current stage of data capability they are at and
what it will require to move to the next stage.

The stages are roughly in order:
- Crawl: Acknowledge data as an asset and discipline. Collect data and catalogue
  it.
- Walk: Use data to power strategic decision making and day to day operations
for us at Bannerflow, we are at the beginning stage of this where what we need
to do is establish our data warehouse and ETL practises
- Run: Close the gap between product teams and data practitioners by embedding
and use data to power product features
- Fly: Deliver data & insights driven product features and projects

## Data platform specifics
At its core a data platform should enable you to create an environment where you
can help the business grow faster. That means building products that are data
driven or building visibility over problems in the business, for example through
exposing some metric etc.


## Vision for role of data and insights
Gathering data is a complex problem. We should ideally not treat data in
isolation. Data is primarily gathered to recreate global context in one place.
This allows the entire company to tap into a single source of truth for the more
disparate use cases: From running an analysis in a operations team to building
new product features. 

At the core of our data is the information produced by our users (In the case of
Bannerflow that would be ad impressions). As this data gets harvested and
collected in our storage layer (Warehouse or lakehouse), we should contextualise
it and build relationships with other datasets, originating from different
product features. Ultimately this results in the global context which constitutes
the foundation of any insights.

We should also do our absolute best to make sure that all the teams at all
levels talk about our business using the same terminology, regardless of country
or role etc.
