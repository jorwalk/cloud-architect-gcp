1.  In your billing project, view billing transaction history. What was your highest cost item so far?

    > From left menu, go to **Billing**, then **Transactions**.

2.  Export your billing data to a Cloud Storage bucket.

    > First create a Cloud Storage bucket from the **Storage** → **Storage** menu; make it a regional bucket and choose your closest region.
    > 
    > Next go back to **Billing** → **Billing Export**.
    > 
    > Click **File Export**.
    > 
    > Type the name of your bucket, enter ‘billing\_export’ in the prefix field, and set **Format** to _CSV_. Then click **Enable Billing Export**.
    > 
    > Be aware that items in the bucket will not show until the next day.

3.  Export billing data to a BigQuery dataset.
    
    > Go to **Billing** → **Billing Export**.
    > 
    > Select the project the BigQuery export will be in.
    > 
    > If prompted, click the **Go to BigQuery** button to create a dataset.
    > 
    > In BigQuery, create a new dataset. Call it 'billing\_export'.
    > 
    > Go back to the Billing Export screen (might have to click browser back button a few times).
    > 
    > Choose project from drop down you just created a dataset in, and the dataset should be automatically found.
    > 
    > Click the **Enable BigQuery export** button.
    > 
    > Again, it will take some time for it to start populating information.

4.  Let’s run some sample queries against a public sample dataset:
    
    > For all queries, go to BigQuery (any project), and click the red **COMPOSE QUERY** button to copy and paste the below queries.
    > 
    > I will provide the SQL queries that you’ll copy and paste into a query field:
    > 
    > First find all charges that were more than 3 dollars:
    > 
    > SELECT product, resource\_type, start\_time, end\_time,  
    > cost, project\_id, project\_name, project\_labels\_key, currency, currency\_conversion\_rate,
    > usage\_amount, usage\_unit
    > FROM \`cloud-training-prod-bucket.arch\_infra.billing\_data\`
    > WHERE (cost > 3)
    > 
    > Next let’s find which product had the highest total number of records:
    > 
    > SELECT product, COUNT(\*)
    > FROM \`cloud-training-prod-bucket.arch\_infra.billing\_data\`
    > GROUP BY product
    > LIMIT 200
    > 
    > Finally, let’s see which product most frequently cost more than a dollar:
    > 
    > SELECT product, cost, COUNT(\*)
    > FROM \`cloud-training-prod-bucket.arch\_infra.billing\_data\`
    > WHERE (cost > 1)
    > GROUP BY cost, product
    > LIMIT 200