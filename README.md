# Serverless with Cosmo DB

In this demo you will create a workflow to to analyze sentiment from Twitter posts. An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.

Start with the tutorial at https://docs.microsoft.com/en-us/azure/azure-functions/functions-twitter-email adn work though these steps:
1. Create a Cognitive Services account
	1. Location is West US
1. Create the function
1. Create a logic app
1. Connect to Twitter
1. Add sentiment detection
1. Connect sentiment output to your function

After we connect the sentiment output with our function, we're going to save this data into **Cosmos DB**


1. Create a database account
1. Create a collection
1. Going back into our Logic App, from the Logic App Designer, click add an action and search for Cosmos
1. Select Create or Update document
	1. If prompted, give a connection name, then get the db Key from the Cosmos DB view in the portal
	1. Enter the database and collection
	1. Add in the JSON syntax below and use the parameters for the values shown.  *To make the GUID, you may have to maximize your browser window as the functionality is hidden*
   
{
  "id": "guid()",
  "loc": "UserDetails.Location",
  "score": "Body",
  "tweet": "OriginalTweet",
  "user": "TweetedBy"
}
   
1. Save the Logic app
1. Click on the first step of the Logic App, and set the interval to 1 minute
1. Verify data is going into Cosmos by using the Data Explorer in the Cosmos Portal View
