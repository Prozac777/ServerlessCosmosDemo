# Serverless with Cosmo DB

In this demo you will create a workflow to to analyze sentiment from Twitter posts. An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.

Start with the tutorial at https://docs.microsoft.com/en-us/azure/azure-functions/functions-twitter-email and work though these steps:
1. Create a Cognitive Services account
    1. Create a new Resource Group that you will use for everything you create in this demo
	1. Location is West US
1. Create the function
1. Create a logic app
1. Connect to Twitter
1. Add sentiment detection
1. Connect sentiment output to your function

After we connect the sentiment output with our function, we're going to save this data into **Cosmos DB**

Follow the first two steps at https://docs.microsoft.com/en-us/azure/cosmos-db/create-documentdb-dotnet and stop at adding sample data

1. Create a database account
1. Create a collection

Now that the database is up...
1. Going back into our Logic App, from the Logic App Designer, click add an action and search for Cosmos
1. Select Create or Update document
	1. If prompted, give a connection name, then get the db Key from the Cosmos DB view in the portal
	1. Enter the database and collection
	1. Add in the JSON syntax below and use the parameters for the values shown.  *To make the GUID, you may have to maximize your browser window as the functionality is hidden*
```
{  
  "id": "guid()",  
  "loc": "UserDetails.Location",  
  "score": "Body",  
  "tweet": "OriginalTweet",  
  "user": "TweetedBy"  
}  
```
1. Save the Logic app
1. Click on the first step of the Logic App, and set the interval to 1 minute
1. Verify data is going into Cosmos by using the Data Explorer in the Cosmos Portal View

Now we will work on visualizing this data with Power BI.  Download and install the desktop app from https://powerbi.microsoft.com/en-us/desktop/

We will use https://docs.microsoft.com/en-us/azure/cosmos-db/powerbi-visualize as a reference for some tasks.

1. Start Power BI Desktop
1. Click Get Data and select Cosmos DB
1. From the Azure Portal, get the URL for your DB and a key for it
1. Select the correct collection, expand the data, and then close and apply
1. Now add a visualization, set it's properties, and test it out
1. When you're done, click Publish. This will prompt you to save it as well
1. Now go to https://powerbi.microsoft.com/en-us/ and log in
1. Then you can take that report and dataset and create a dashboard
