MainScreen
Methods to interact with the MainScreen.

ObjectFinder.Unlimit
procedure TRSObjectFinder.Unlimit;
Resets ObjectFinder size limits

ObjectFinder.Unlimited
function TRSObjectFinder.Unlimited: TRSObjectFinder;
Returns a copy of the ObjectFinder with the size limits removed.

MainScreen.FilterInPolygon
function TRSMainScreen.FilterInPolygon(tpa, polygon: TPointArray): TPointArray;
function TRSMainScreen.FilterInPolygon(atpa: T2DPointArray; polygon: TPointArray): T2DPointArray; overload;
Filters the given TPointArray or T2DPointArray and returns only those that are visible within a polygon on the mainScreen.

MainScreen.GetAdjacentTiles
function TRSMainScreen.GetAdjacentTiles: TRectArray;
Returns the 4 tiles adjacent to the player in form of a TRectArray.

MainScreen.DebugAdjacentTiles
procedure TRSMainScreen.DebugAdjacentTiles;
Debugs MainScreen.GetAdjacentTiles.

Example:

MainScreen.DebugAdjacentTiles;
MainScreen.InMultiCombat
function TRSMainScreen.InMultiCombat: Boolean;
Returns true if we are in multi combat false if not.

Example:

Writeln MainScreen.InMultiCombat;
MainScreen.FindGrave
function TRSMainScreen.FindGrave: Boolean;
Returns true if we died and there’s a grave available somewhere, false otherwise.

Example:

Writeln MainScreen.FindGrave;
MainScreen.LoadingPOH
function TRSMainScreen.LoadingPOH: Boolean;
Returns true if we are loading a poh.

Example:

Writeln MainScreen.LoadingPOH;
MainScreen.WaitLoadingPOH
function TRSMainScreen.WaitLoadingPOH: Boolean;
Waits for the POH loading screen returns true if we find a loading screen and successfully wait for it to finish.

Example:

Writeln MainScreen.WaitLoadingPOH;
MainScreen.FindEnemyHitsplats
function TRSMainScreen.FindEnemyHitsplats(): Boolean;
Returns the hitsplats on screen that don’t belong to the player.

Example:

Debug(MainScreen.FindEnemyHitsplats());
MainScreen.InCombat
function TRSMainScreen.InCombat: Boolean;
Returns true if we are currently in combat. With slow attack speed between you and the enemy this might return false negatives.

Example:

Writeln MainScreen.InCombat;
MainScreen.WaitInCombat
function TRSMainScreen.WaitInCombat(waitTime: Int32; interval: Int32 = -1): Boolean;
Waits the specified waitTime until we are in combat.

Example:

MainScreen.WaitInCombat(5000);
MainScreen.WaitNotInCombat
function TRSMainScreen.WaitNotInCombat(waitTime: Int32; interval: Int32 = -1): Boolean;
Waits the specified waitTime until we are nto in combat.

Example:

MainScreen.WaitNotInCombat(5000);
MainScreen.FindArrow
function TRSMainScreen.FindArrow(out TPA: TPointArray): Boolean;
function TRSMainScreen.FindArrow: Boolean; overload;
Returns true if there’s a yellow arrow on screen. If a TPointArray is passed as a parameter it will return with the location of the arrow tip.

Example:

Writeln MainScreen.FindArrow;
MainScreen.WaitArrow
function TRSMainScreen.WaitArrow(TPA: TPointArray; WaitTime: Int32 = 600; Interval: Int32 = -1): Boolean;
function TRSMainScreen.WaitArrow(WaitTime: Int32 = 600; Interval: Int32 = -1): Boolean;
Waits WaitTime for a yellow arrow to appear on MainScreen. If a TPointArray is passed as a parameter it will return with the location of the arrow tip.

Example:

Writeln MainScreen.WaitArrow;