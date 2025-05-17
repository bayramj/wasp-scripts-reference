TRSFishingHandler
TRSFishingHandler is a full color fishing bot that is highly customizable.

TRSFishingHandler.Setup
procedure TRSFishingHandler.Setup();
Resets TRSFishingHandler to the non fishing state. This will:

Pause TRSFishingHandler.Timer;

Reset TRSFishingHandler.CurrentSpot;

Set TRSFishingHandler.IsFishing to False;

TRSFishingHandler.Reset
procedure TRSFishingHandler.Reset();
Resets TRSFishingHandler to the non fishing state. This will:

Pause TRSFishingHandler.Timer;

Reset TRSFishingHandler.CurrentSpot;

Set TRSFishingHandler.IsFishing to False;

TRSFishingHandler.GetMMShoreLine
function TRSFishingHandler.GetMMShoreLine(): TPointArray;
Get the shore lines on the minimap.

Example:

ShowOnClient(TRSFishingHandler.GetMMShoreLine());
TRSFishingHandler.GetMSShoreLine
function TRSFishingHandler.GetMSShoreLine(): TPointArray;
Get the shore lines on the mainscreen.

Example:

ShowOnClient(TRSFishingHandler.GetMSShoreLine());
TRSFishingHandler.FindWaterDirection
function TRSFishingHandler.FindWaterDirection(): TRectangle;
Finds the adjacent tile that is directly close to the player that has water.

Example:

ShowOnClient(TRSFishingHandler.FindWaterDirection(), False);
TRSFishingHandler.FindSpot
function TRSFishingHandler.FindSpot(out atpa: T2DPointArray; waitTime: Int32 = 350): Boolean;
function TRSFishingHandler.FindSpot(): Boolean;  overload;
Find fishing spots on the mainscreen. Optionally return at ATPA of the found spots.

Example:

var
  atpa: T2DPointArray;
begin
  if TRSFishingHandler.FindSpot(atpa) then //TRSFishingHandler.FindSpot() returns true/false.
    ShowOnClient(atpa);
end;
TRSFishingHandler.WaitSpot
function TRSFishingHandler.WaitSpot(out atpa: T2DPointArray; waitTime: Int32 = 350): Boolean;
function TRSFishingHandler.WaitSpot(): Boolean;  overload;
Wait for fishing spots on the mainscreen. Optionally return at ATPA of the found spots.

Example:

var
  atpa: T2DPointArray;
begin
  if RSFishingHandler.WaitSpot(atpa) then //TRSFishingHandler.FindSpot() returns true/false.
    ShowOnClient(atpa);
end;
TRSFishingHandler.SpotMoved
function TRSFishingHandler.SpotMoved(out atpa: T2DPointArray): Boolean;
function TRSFishingHandler.SpotMoved(): Boolean;  overload;
Check if TRSFishingHandler.CurrentSpot moved.

Example:

WriteLn TRSFishingHandler.SpotMoved();
TRSFishingHandler._StoppedFishing
function TRSFishingHandler._StoppedFishing(): Boolean;
Internal helper method to check for quick things that guarantee us we are not fishing anymore.

TRSFishingHandler.CheckFishing
function TRSFishingHandler.CheckFishing(out atpa: T2DPointArray): Boolean;
function TRSFishingHandler.CheckFishing(): Boolean;  overload;
Check if we are still fishing. This function could give false positives but it’s extremely unlikely. To determine if we are still fishing it does the following:

Check if TRSFishingHandler.CurrentSpot (which is the last spot we clicked) has moved.

Check if the inventory is full.

Check if we leveled up.

Check if TRSFishingHandler.Timer has reached it’s end. The time lasts anywhere between 40 seconds and 70 seconds randomly and it’s reset everytime this is called and we earned XP.

Example:

WriteLn TRSFishingHandler.CheckFishing();
TRSFishingHandler.FacingWater
function TRSFishingHandler.FacingWater(): Boolean;
Check if we have water directly north, west, south or east of us.

Example:

WriteLn TRSFishingHandler.FacingWater();
TRSFishingHandler.ClickSpot
function TRSFishingHandler.ClickSpot(out atpa: T2DPointArray): Boolean;
function TRSFishingHandler.ClickSpot(): Boolean;  overload;
Click the closest fishing spot to the player and switches TRSFishingHandler to “IsFishing”. We can check if we are still fishing with TRSFishingHandler.CheckFishing().

Example:

TRSFishingHandler.ClickSpot();