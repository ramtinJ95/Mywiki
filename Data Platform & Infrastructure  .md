# Data Platform & Infrastructure

## Evergreen Data Platform & Infrastructure Fundamentals
The four basic or key layers of a data platform are:
- Data pipelines, this is ETL/ELT
- Orchestration, this can be sometimes combined with pipelines 
- Data storage
- BI/Data Science

#### Data pipelines and Ingestion - Getting data into your system
This is the process of moving data from various sources, i.e logs, third party
aps/ api's, OLTP systems etc, into your analytics environment.

The three approaches for this is:
- Fully custom code for the entire process
- Low code ingestion tools such as Fivetran, Mattilion etc.
- Code based frameworks such as Prefect, Dagster and Airflow. These tools gives
  alot of control and help orchestrate complex multi step pipelines.

Now each of these options usually also nowdays makes use of a transformation
tool such as dbt or sqlmesh.

#### Data storage - Building a central source truth
The analytics environment mentioned above is referencing essentially this
storage layer. This could be either a data warehouse, date lake or a lakehouse.
The main idea here is that we want a centralized data layer where teams can work
from the safe definitions, metrics and logic. So instead of team members going
and pulling data themselves from different sources they can just come and join
in whatever it is that they need directly in the storage layer. Thus a good
storage layer unlocks:
- Standardized data models
- Governance and access control
- Data Quality and consistency
- Faster time to insight

#### Data visualization - Turning data into decisions
Ingestion and storage are necessary but not enough. To drive impact and actually
solve problems people actually need to use the data.

Dashboards, KPI's. self-service tools, and even excel reports are all ways teams
consume and make decisions. When done right, reporting provides:
- Executives with clarity
- Enable eams to track initiatives
- Help analysts test hypotheses

The ultimate goal is to build reports that are trusted, actionable and aligned
with how your business operates

#### Data science and Notebooks
While dashboards are built for monitoring and decision-making, data science tools support exploration, experimentation, and advanced analysis. This is where notebooks and model development environments come in.

Not every company needs machine learning from day one. But as your data maturity grows, you’ll likely want to go beyond just looking at the past, you’ll want to forecast, segment, classify, or personalize based on that data.

Notebooks are ideal for:
- Prototyping models quickly
- Exploring data visually with Python, R, or SQL
- Combining code, charts, and documentation in one place
- Sharing insights across teams or stakeholders
They’re especially useful for cross-functional work, where a data scientist wants to show not just the results, but how they got there.

Use cases for this layer:
- Customer segmentation
- Predictive modeling (churn, sales, etc)
- Experiment analysis (churn, sales, etc)
- Time series forecasting
- NLP for inernal documents or chat data

Think of notebooks as the R&D lab of your data stack. They don’t replace pipelines or BI, they complement them by enabling deeper questions and experimentation.

As your team matures, this layer becomes more important not just for data scientists, but for analysts and product teams who want to explore without committing to production changes right away.

## Patterns

## Best Practice
