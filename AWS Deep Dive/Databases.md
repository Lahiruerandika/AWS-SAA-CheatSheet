# Databases

## Choosing the Right Database

There are several databases on AWS to choose from. Below are some guiding questions to help select the best database for your product:

- Is the workload read-heavy, write-heavy, or balanced? What are the throughput needs? Will the throughput change, fluctuate, or require scaling over time?
- How much data will be stored, and for how long? Will the data size grow? What is the average size of an object in the database? How frequently are these objects accessed?
- Data durability: Should the data be stored for a short period (e.g., a week) or permanently? Will the database serve as a source of truth?
- What are the latency concerns?
- What is the data model? How will the data be queried? Will the data be structured, semi-structured, or unstructured?
- Do we need a strict schema or a flexible schema? Do we require reporting capabilities or advanced search functionality?
- What are the licensing costs? Can we switch to a cloud-native database such as Aurora or DynamoDB?

