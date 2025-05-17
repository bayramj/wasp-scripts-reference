WorldHopper
Made by @Yolandi, modified by @Torwent.

World hopper is resposible for hopping worlds with the logged in world hopper in the logout tab.

type TRSWorldHopper
type
  TRSWorldHopper = record(TRSInterface)
    SILVER, YELLOW: Int32;
    ReadyTime: UInt64;
  end;
WorldHopper record.

TRSWorldHopper.Setup
procedure TRSWorldHopper.Setup(); override;
Internal method used to setup the WorldHopper.

TRSWorldHopper.Scroll
procedure TRSWorldHopper.Scroll(down: Boolean);
Scroll one page up or down of the world hopper.

Example:

TRSWorldHopper.Scroll(True);
TRSWorldHopper.ClickWorld
procedure TRSWorldHopper.ClickWorld(ocrBounds: TBox);
Click a world in the world hopper.

Example:

TRSWorldHopper.ReadWorlds(ocrBounds);
TRSWorldHopper.ClickWorld(ocrBounds[0]);
TRSWorldHopper.GetCurrentWorld
function TRSWorldHopper.GetCurrentWorld(): Int32;
Returns the current world we are on.

Example:

WriteLn TRSWorldHopper.GetCurrentWorld();
TRSWorldHopper.ReadWorlds
function TRSWorldHopper.ReadWorlds(out boxes: TBoxArray): TIntegerArray;
function TRSWorldHopper.ReadWorlds(): TIntegerArray;  overload;
Returns currently visible worlds.

Example:

WriteLn TRSWorldHopper.ReadWorlds();
TRSWorldHopper.WaitForHop
function TRSWorldHopper.WaitForHop(world: Int32; ocrBounds: TBox; coolDownOnFail: Boolean=True): Boolean;
Exits false if “Please wait” not found, presumably due to combat.

TRSWorldHopper.Hop
function TRSWorldHopper.Hop(targetWorlds: TIntegerArray): Boolean;
Hops to a different world from the specified targetWorlds.

Example:

WriteLn TRSWorldHopper.Hop([303, 304, 305]);