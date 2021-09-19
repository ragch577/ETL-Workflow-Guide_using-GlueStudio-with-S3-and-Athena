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
 
# Step 3: Define the Glue job
# Step 4: Query the data with Athena
