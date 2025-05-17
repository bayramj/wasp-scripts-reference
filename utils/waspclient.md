HTTPClient
Wrapper type with methods to interace with built in Simba http features.

WaspClient
Responsible for connecting to waspscripts.com database. Because of the way Simba HTTPClients work, it’s easier to have different clients for different servers when they use different headers.

There’s some bug that makes it required to “refresh” the client after logging in. Oh Simba… you never stop surprising me.

TWaspClient.CheckRoleAccess
function TWaspClient.CheckRoleAccess(): Boolean;
This queries the /roles endpoint on WaspScripts database to determine if the user has any roles which grant automatic script access. Returns True/False based on the user’s role. Modified based on WaspLauncher source.

TWaspClient.GetSubscriptions
function TWaspClient.GetSubscriptions(): TSubscriptionDataArray;
This queries the /subscriptions endpoint on WaspScripts database to create an array of all active subscriptions the user has. Modified based on WaspLauncher source.

TWaspClient.GetFreeAccess
function TWaspClient.GetFreeAccess(): TSubscriptionDataArray;
This queries the /free_access table on WaspScripts database to create an array of all granted access the user has. Modified based on WaspLauncher source.

tSubscriptionDataArray._MatchProduct
function tSubscriptionDataArray._MatchProduct(product : String; out MatchedProduct : tSubscriptionData): Boolean;
A helper function that searches the tSubscriptionDataArray for the matching product. Returns True/False to identify if a product was matched. out MatchedProduct is the tSubscriptionData for the product ID that matched.

TWaspClient.GetProductCode
function TWaspClient.GetProductCode(scriptID : String): String;
A function which converts a script ID to product code. In some tables, only the script ID is given, and in other tables only the product code is given. This is required to ensure all functions are comparing the same identifier.

TWaspClient.GetProductLink
function TWaspClient.GetProductLink(ScriptID : String): String;
A function which looks up a given script ID and returns the URL to that script’s WaspScripts page.

TWaspClient.ExplodeBundles
function TWaspClient.ExplodeBundles(subs : tSubscriptionDataArray): tSubscriptionDataArray;
This function looks up all bundles in the WaspScripts database, and compares them against the subscriptions subs argument. Any bundles in the subs array will be decomposed to the constituent scripts. The Result is only the exploded bundle and does not include the originally input subs
