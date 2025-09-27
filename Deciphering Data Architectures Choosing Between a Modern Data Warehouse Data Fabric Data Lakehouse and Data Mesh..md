## Notes From The Book

### Modern Data Warehouse overview
insert pic here

### Lakehouse overview
insert pic here

- page 47, Descriptive and diagnostic analytics 
- How to determine what has changed since last data extraction: Timestamps, cdc,
  partionining: some source systems use range partionining, in which the source
  tables are partitioned alng a date key. For example if you are extractingafrom
  an orders table partioned by day, it is easy to identify the current or
previous days data. Other methods of detection are: Database triggers, merge
staements. Merge statement approach is owrst because its a full dump of source
systems, then a potentially huge diff operation in the data warehouse.
- Explain clearly schema on read vs schema on write
- Data lake is a bottom-up to data managment. while a traditional relation data
  warehouse is a top-down approach. Main difference is that a lake requires no
upfront work and is ideal for situations where we dont know what questions to
ask yet.
- page 62-63 predictive and prescriptive analysis
- page 71 multiple data lakes. It just feels wrong but could potetially be valid
  if data has to be seperated by region for example etc.
- page 76-78 about data marts and ODS was good.
- page 83-85 abput data virtualization is very interesting, the idea is quite
new to me
- page 91, the difference between data design and data modelling was great.
- Chapter 8 was quite weak
- chapter 9 nothing new for me
- Side note while reading: I think given the limited expertise and experience
the MDW artchitecture is the best one for us. We can always migrate to a full
lakehouse model later since much of the foundation is shared between the two
architectures.
- Figure 10.2 page 138 is great for MDW explanation
- page 140-141 pros and cons for MDW
- chapter 11 quite weak
- figure 12.1 page 160 is great
- Skills needed for building the data platform:
  - Data Architect
  - Data Engineer
  - Data Scientist
  - Analyst's. Business, analytics engineer etc.
- Risks when building a new data platform:
  - Thinking BI is easy
  - Too many or too few business requirements
  - Structuring the DW to reflect source data rather than the business needs
  - Presenting the end users with a solution that is slow or has bad performance
  - Not involving users, showing them results and getting them excited

---
[status](status): :📖:
tags: [[Book notes]] - [[030 Software Development.md]] - [[001 Book Index.md]]
date: 2025-09-27
