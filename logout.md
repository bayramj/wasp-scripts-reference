Logout
Extends SRL’s TRSLogout.

Logout.ClickLogout
function TRSLogout.ClickLogout(attempts: Int32 = 5; time: Int32 = 20000): Boolean; override;
Clicks the logout button. Returns true if we succesfully logout of the game. Depending on the account biohash it might use the start buttons to rate the game.

Example:

WriteLn Logout.ClickLogout();