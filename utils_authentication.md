Authentication
Uses tWaspClient to determine if a user is subscribed to the active script and displays a warning if the subscription is inactive.

The procedure which runs when the Go to Script Page button is clicked.

This procedure updates the countdown on the Run Anyway button

TWaspClient.GetScriptInfo
function TWaspClient.GetScriptInfo(ScriptID : String): tScriptData;
A function which looks up a given script ID and returns the script data.

TWaspClient.HasAccess
function TWaspClient.HasAccess(scriptID : String) : Boolean;
This function checks whether the current User has access to the given Script ID. Returns True if the User has access.

TWaspClient.CheckSubscription
procedure TWaspClient.CheckSubscription(UseTimer : Boolean = True);
Checks whether the user is subscribed to the current script. If not, the Access Warning Form is shown.