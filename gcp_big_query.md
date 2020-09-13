# Google Cloud Fundamentals: Getting Started with BigQuery

# Objectives

# Load data from Cloud Storage into BigQuery.

# Perform a query on the data in BigQuery.

Step 1 : Load data from Cloud Storage into BigQuery

1. on the Navigation menu , click BigQuery then click Done.

2. Create a new dataset .

3. Insert dataset id.

4. Creating a data location close to you.

5. Create a new table in the "dataset" to store the data from the CSV file.

6. Click Create Table. On the Create Table page

7. Select the source section.

Step 2 : Perform a query on the data using the BigQuery web UI

1. In the Query editor window, a query to discover the data can be used.

   select int64_field_6 as hour, count(\*) as hitcount from logdata.accesslog
   group by hour
   order by hour

2. Click run
