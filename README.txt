TwitterStreamClient

An API for parsing Twitters real-time public streaming API.

No oath support yet. The public streaming API says the traditional
username/password will be deprecated at some point. But not yet.

How to use:

// create a string with your credentials
// if you provide an encrypted password, set the flag
TwitterStream stream = new TwitterStream (user, pass, isEncrypted);
			
// Optional: Add a filter. If filtering,
// the Twitter API requires to specify at least 1 parameter
TwitterStreamFilter filter = new TwitterStreamFilter ();
string[] keywords = { "twitter", "pizza"};
filter.setTrackingKeywords (keywords);
// to remove the filter, set it to null
stream.SetStreamFilter (filter);
			
stream.StartAsyncStream ();
			
while (stream.IsStreamRunning() && (numberOfTweets != 0)) {
	Status status = stream.GetBlockingNextStatus ();

	// make sure to handle deleted statuses which appear in
	// public stream
	if (status.text != null) {
		Console.Write("@" + status.user.screen_name + ": ");
		Console.WriteLine (status.text);
			
		numberOfTweets--;
	}
}
			
// make sure to clean up
stream.StopAsyncStream ();

This sample is provided in Program.cs

If you would like to produce a DLL for use in your projects,
change the build settings of your solution to Library.

If you want to run the code in Program.cs, 
change the build settings to Executable.