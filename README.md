# Step 1: Create a bucket
- Create bucket customer-bkt
- Uplaod Customer csv file into bucket.
# Step 2: Define the Crawler using AWS Glue.
- To add Crawler to my S3 datastore:
  - I give Crawler the name customer-crawler, and click next.
  - Keeping the Crawler source type on the default settings, I click next again.
  - I select S3 as the datastore and specify the path of customer-bkt, and click next. (Note: here, if you want to add a connection, you have to complete the S3 VPC endpoint set up)
  - I select an existing IAM (Identity and Access Management) role radio button. Then, to create an IAM role, I go to the IAM Console, which will direct me to the IAM Management Console.
      - Click create a role.
      - Select Glue under the use cases, and click next.
      - Tick administrator accessunder the permission policies, and click next.
      - Give a preferred role name, and click the create-role button.
  - Now, let’s come back to the Crawler creation. Select the created IAM role from the dropdown and click next.
  - Set the frequency as run on demand and click next. (If needed, you can schedule your Crawler hourly, daily, weekly, monthly, etc.)
  - To store the Crawler output, I create a database called employee-database, select the created database from the dropdown, and click next.
  -  Finally, review all the settings that have been configured, and click finishto create the Crawler.
  -  Now that the Crawler has been created click customer-crawler and run it. If the Crawler job status changes from starting-status to stopping-status to ready-status, the Crawler job has been successful.
  -  The Crawler job will automatically create the tables in our database. It will also automatically detect the number of columns on our CSV file and their data types.
  -  If the Crawler job ends up with an endpoint error:
  -  Check that you have an Amazon S3 VPC endpoint set up, which is required with AWS Glue. If you haven’t set up VPC previously, here’s how
     - Go to the Amazon VPC Console and select endpointsunder the virtual private cloud.
     - Click create an endpoint, select com.amazonaws.eu-west-1.acm-pca under the service names and take the default options for the rest. 
# Step 3: Define the Glue job
-  Open AWS glue studio and click jobs.
-   I select Source and target added to the graph and it will direct us to a canvas where we can define source to target mapping. Here remember to give a name (in my case employee job) for the Glue job, otherwise, it will return an error.
-   To define source to target mapping:
   - I click data source and select the source database and the table.
   - Then, I click transform and give the transform logic as select fields and select the id and name fields from the transform tab.
   - Finally, I click data target and specify the target path. (I created a new S3 bucket called target-customer-bkt.)
   - I click job details and select the IAM role which we created in Step 2.
   - Now we can save the job and run.
# Step 4: Query the data with Athena
- AWS Athena is the query service that AWS offers to analyze data in S3 using standard SQL. In this tutorial, I use Athena to query the ETL data and perform some SQL query operations. In AWS Management Console, we can search for Athena, and there you can see the medium-bkt table which is automatically created while we perform the ETL to employee-database.
- But before running my first query, I need to set up a new bucket in S3 to store the query output. So, I go back to the S3 dashboard and create a new folder called query-output inside my customer-bkt. I then come back to Athena and specify the path of the query result location as shown below.
- Finally, now I can either query my source and target table and see the results, or analyze the data using SQL queries.
