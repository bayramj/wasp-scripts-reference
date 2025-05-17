Walker Objects
Methods to handle TRSWalkerObjects. TRSWalkerObject can be anything that you want to interact with on the mainscreen. They are divided in 2 main categories and one of them in 3 sub-categories but the usage is only limited by your imagination:

RSObjects (TRSWalkerObjects that don’t have a dot on the minimap)

MMDots: (TRSWalkerObjects that have a dot on the minimap) -RSNPCs -RSGroundItems -RSPlayers

How do they work?
TRSWalkerObjects are very customizable and can be used to interact with almost everything. For some niche use cases it might be worth do something custom or override some methods to get the behavior you want.

The default way they work is:

WaspLib checks if you are in the TRSWalkerObject.Coordinates range. If not and you used one of the Walk methods, it will walk to that location.

Being in the TRSWalkerObject location, then we check if our TRSWalkerObject is a TRSObject or a TRSMMDot. for a TRSObject we stick with the TRSWalkerObject.Coordinates, for TRSMMDots, the coordinates are changed to the minimap dots that within the radius specified when the TRSWalkerObject was setup.

WaspLib then convert the coordinate along with the TRSWalkerObject.ShapeArray information to a TCuboidArray on the mainscreen (https://en.wikipedia.org/wiki/Cuboid).

This TCuboidArray is the “bounds” of our targets. Each one should accurately surround each of our possible targets.

Then WaspLib runs MainScreen.FindObject() inside of each TCuboid. For more info on how this works read the TRSObjectFinder documentation (https://torwent.github.io/SRL-T/mainscreen.html#type-trsobjectfinder).

An ATPA of the found colors inside each cuboid is then returned.

If the method used is related to hovering or clicking, we hover the closest target and then check if TRSWalkerObject.UpText matches the uptext.

If it does and we are using a clicking method, we click it.

If we use a select method, if the option is not in the uptext we right click the target and select that option.

This is the default behavior but TRSWalkerObjects are very customizable and functionality can be toggled on with TRSWalkerObject.Filter:

Filter.Walker: Disables walker for the TRSWalkerObject. Coordinates are ignored and still use the minimap dots that are visible on the minimap if we are talking about a TRSMMDot, otherwise only MainScreen.FindObject() is used.

Filter.MinimapDot: Disables the usage of minimap dots for TRSMMDots. TRSObjects have this off by default. Disabling this for TRSMMDots is only useful if the the Player, NPC or Item is in a fixed position.

Filter.Finder: Disables color checking. The returned cuboids by Walker and MM2MS are our targets. This is useful for things that are “invisible” like agility shortcuts and/or things that have colors that are just unreliable.

UpText: Ignore all uptext when hovering the targets

Filter.Skip: This is an internal filter that you probably don’t want to use directaly. Decides which TRSWalkerObjects setup is skipped during wasplib’s setup process.

Note

You cannot disable Filter.Walker, Filter.MinimapDot, Filter.Finder all at the same time. You need one of them enabled and keep in mind that TRSObjects already have Filter.MinimapDot disabled.

type TRSWalkerObject
TRSWalkerObject = record
  Filter: record
    Walker:     Boolean;
    MinimapDot: Boolean;
    Finder:     Boolean;
    UpText:     Boolean;
    Skip:       Boolean;
  end;

  ShapeArray: TRSMainScreenShapeArray;
  Coordinates: TPointArray;

  Finder: TRSObjectFinder;
  UpText: TStringArray;
  ActionUpText: TStringArray;
class var
  CurrentUpText: TStringArray;
  CurrentActionUpText: TStringArray;
  RedClicked: Boolean;
end;

PWalkerObjectArray = array of Pointer;
PRSWalkerObject = ^TRSWalkerObject;
Parent record of all TRSWalkerObjects.

Walker.Click
function TRSWalker.Click(minimapPoint: TPoint; Randomness: Int32): Boolean; override;
You shouldn’t modify this unless you know what you are doing, otherwise you might break TRSWalkerObjects. This is overriden so if we redclick our current TRSWalkerObject target while mainscreen walking we disable walker. When we start the walking process towards a TRSWalkerObject, TRSWalkerObject.CurrentUpText is temporarily set so we know what we are looking for while walking. Once we click the target TRSWalkerObject.CurrentUpText is cleared.

TRSWalkerObject._Setup
procedure TRSWalkerObject._Setup();
Base internal TRSWalkerObject setup method. You probably won’t need to call this directly, it’s called by the next setup methods automatically.

TRSWalkerObject.Setup
procedure TRSWalkerObject.Setup(coordinates: TPointArray);
procedure TRSWalkerObject.Setup(upText: TStringArray); overload;
TRSWalkerObject setup methods. You usually need to call of this.

The method that takes in coordinates should be called first. That is because TRSWalkerObject.Setup(coordinates: TPointArray) is where we decide if TRSWalkerObject.Filter.Skip is going to be true or not.

Keep in mind if you don’t use a TRSWalker in your script and want to use TRSWalkerObjects, you will need to manually setup them in your script because they will all be skipped. So you need to set TRSWalkerObject.Filter.Skip := False and then call TRSWalkerObject.Setup(upText: TStringArray)

Normal usage in the following example.

Example:

//Example with walker:
var
  rsw: TRSWalker;
  obj: TRSObject; //This is a type of TRSWalkerObject.
begin
  rsw.Setup();
  obj.Setup([[200, 200]]);
  obj.Setup(['My', 'uptext']);
end;

//Example without walker:
var
  obj: TRSObject; //This is a type of TRSWalkerObject.
begin
  obj.Setup(['My', 'uptext']);
end;
TRSWalkerObject.GetCuboidArray
function TRSWalkerObject.GetCuboidArray(): TCuboidArray;
Internal TRSWalkerObject method responsible for returning a TCuboidArray of our target on the 3D world (on mainscreen and outside of it). You will probably never need to use this directly. You can visually see this in action by using the Debug() methods, this is responsible for the white lines surounding the targets.

TRSWalkerObject.FindOnMainScreen
function TRSWalkerObject.FindOnMainScreen(cuboidArray: TCuboidArray): T2DPointArray;
Internal TRSWalkerObject method responsible for filtering a TCuboidArray by what’s visible in the mainscren. This is meant to filter TRSWalkerObject.GetCuboidArray() so targets that are outside of the mainscreen are filtered out. You will probably never need to use this directly.

TRSWalkerObject.OnMainScreen
function TRSWalkerObject.OnMainScreen(cuboidArray: TCuboidArray): Boolean;
Internal TRSWalkerObject method that returns true or false if we have TCuboids visible on the mainscreen. You probably don’t need to use this directly.

TRSWalkerObject._UpTextCheck
function TRSWalkerObject._UpTextCheck(out shouldExit: Boolean): Boolean;
Internal TRSWalkerObject helper method that is used by all hovering methods. You probably don’t need to use this directly.

TRSWalkerObject._WalkUpTextCheck
function TRSWalkerObject._WalkUpTextCheck(out shouldExit: Boolean): Boolean;
Internal TRSWalkerObject helper method that is used by all walking hover methods. You probably don’t need to use this directly.

TRSWalkerObject._ClickHelper
function TRSWalkerObject._ClickHelper(leftClick: Boolean): Boolean;
Internal TRSWalkerObject helper method that is used by other clicking methods. You probably don’t need to use this directly.

This is what’s responsible for deciding if we click a target we are hovering or not.

TRSWalkerObject._SelectHelper
function TRSWalkerObject._SelectHelper(action: TStringArray): Boolean;
Internal TRSWalkerObject helper method that is used by other select methods. You probably don’t need to use this directly.

This is what is responsible for deciding if we just left click a target we are hovering or right click it and choose an option.

type TRSObject
TRSObject = type TRSWalkerObject;
TRSObjectArray = array of TRSObject;
PRSObject = ^TRSObject;
PRSObjectArray = array of PRSObject;
TRSObjects are a type of type TRSWalkerObject. This are meant to be TRSWalkerObjects that do not have a minimap dot so TRSObject.Filter.MinimapDot is False by default and shouldn’t be changed.

TRSObject.Setup
procedure TRSObject.SetupEx(shape: Vector3; coordinates: TPointArray); overload;
procedure TRSObject.Setup(size, height: Double; coordinates: TPointArray); overload;
procedure TRSObject.Setup(height: Double; coordinates: TPointArray); overload;
All this extend the basic TRSWalkerObject.Setup(coordinates: TPointArray). For TRSObjects this are the methods that should be used for setting them up initially.

In TRSObject.Setup(shape: Vector3; coordinates: TPointArray), shape should be a vector3 of the object shape in number of tiles:

shape.X: number of tiles of the object from west to east.

shape.Y: number of tiles of the object from north to south.

shape.Z: object height, this value has to be guessed, I recommend you try several values and debug it until it looks good to you. As some examples, player and npcs height is around 7, bank chests 4, yew/magic trees 14/16.

In TRSObject.Setup(size, height: Double; coordinates: TPointArray), size and height are used to create a Vector3 “shape” and call TRSObject.Setup(shape: Vector3; coordinates: TPointArray). In this case, shape.X and shape.Y would be both equal to size.

Lastly, TRSObject.Setup(height: Double; coordinates: TPointArray) also calls TRSObject.Setup(shape: Vector3; coordinates: TPointArray) and sets the shape.X and shape.Y to 1.

TRSObject.Find
function TRSObject.FindEx(out cuboids: TCuboidArray; out atpa: T2DPointArray): Boolean;
function TRSObject.Find(out atpa: T2DPointArray): Boolean;
TRSObject method used to find a type TRSObject. If found returns true, if not returns false. The “extended” method in particular is mostly meant for debugging and is the one used when you call Debug(TRSObject).

Example:

WriteLn RSObjects.GEBank.Find(atpa); //Be in ge and with a walker setup there.
Debug(atpa);
TRSObject.IsVisible
function TRSObject.IsVisible(): Boolean;
TRSObject method used to find a type TRSObject. If found returns true, if not returns false.

Example:

WriteLn RSObjects.GEBank.IsVisible(); //Be in ge and with a walker setup there.
TRSObject.FindFromPosition
function TRSObject.FindFromPosition(me: TPoint; out atpa: T2DPointArray): Boolean;
Look for a type TRSObject as if you were on a different position. Great for things like pre-hovering.

TRSObject.Draw
procedure TRSObject.Draw(out bitmap: TMufasaBitmap);
Internal method used to draw found TRSObjects in a TMufasaBitmap.

Example:

Bitmap.FromClient()
RSObjects.GEBank.Draw(Bitmap); //Be in ge and with a walker setup there.
Bitmap.Debug();
Bitmap.Free();
TRSObject.SaveDebug
procedure TRSObject.SaveDebug();
Saves a debug image of the TRSObject to Simba\Screenshots\RSObjects

Example:

RSObjects.GEBank.SaveDebug(); //Be in ge and with a walker setup there.
TRSObject._UpdateTarget
procedure TRSObject._UpdateTarget(sender: PMouse; var x, y: Double; var done: Boolean);
Internal helper method of TMouseMovingEventEx type used to update the target position while the mouse is moving. You should probably not touch this if you don’t understand it.

TRSObject._HoverHelper
function TRSObject._HoverHelper(attempts: Int32; trackTarget: Boolean): Boolean;
Internal helper method used to hover a TRSObject target. You should not use this directly.

TRSObject._WalkHoverHelper
function TRSObject._WalkHoverHelper(attempts: Int32; trackTarget: Boolean): Boolean;
Internal helper method used to walk and hover a TRSObject target. You should not use this directly.

This is responsible for deciding wether we should walk to a TRSObject target or not before attempting to hover it.

TRSObject.PreHoverHelper
function TRSObject.PreHoverHelper(attempts: Int32): Boolean;
Internal helper method used to pre-hover a TRSObject target. You should not use this directly.

TRSObject.Hover
function TRSObject.Hover(attempts: Int32 = 2; trackTarget: Boolean = TRACK_TARGET): Boolean;
Method used to hover a TRSObject target if it’s found on the mainscreen. It can update the target position while the mouse moves with trackTarget.

Example:

RSW.WebWalk(WaspWeb.LOCATION_VARROCK);
RSObjects.GEBank.Hover(); //Be in GE with a walker setup there.
TRSObject.WalkHover
function TRSObject.WalkHover(attempts: Int32 = 2; trackTarget: Boolean = TRACK_TARGET): Boolean;
Method used to walk and hover a TRSObject target if it’s found on the mainscreen after walking. It can update the target position while the mouse moves with trackTarget.

Example:

//Be in varrock with a varrock map loaded.
RSW.WebWalk(WaspWeb.LOCATION_VARROCK);
RSObjects.GEBank.WalkHover();
TRSObject.Click
function TRSObject.Click(leftClick: Boolean = True; attempts: Int32 = 2): Boolean;
Method used to click a TRSObject target if it’s found on the mainscreen.

Example:

//Be in ge with a ge map loaded.
WriteLn RSObjects.GEBank.Click();
TRSObject.SelectOption
function TRSObject.SelectOption(action: TStringArray; attempts: Int32 = 2): Boolean;
Method used to select an option on a TRSObject target if it’s found on the mainscreen.

Example:

//Be in ge with a ge map loaded.
WriteLn RSObjects.GEBank.SelectOption(['Collect']);
TRSObject.WalkClick
function TRSObject.WalkClick(leftClick: Boolean = True; attempts: Int32 = 2): Boolean;
Method used to walk and click a TRSObject target if it’s found on the mainscreen.

Example:

//Be in ge with a ge map loaded, preferably far away so it has to walk.
WriteLn RSObjects.GEBank.WalkClick();
TRSObject.WalkSelectOption
function TRSObject.WalkSelectOption(action: TStringArray; attempts: Int32 = 2): Boolean;
Method used to walk and select an option on a TRSObject target if it’s found on the mainscreen.

Example:

//Be in ge with a ge map loaded, preferably far away so it has to walk.
WriteLn RSObjects.GEBank.WalkSelectOption(['Collect']);
type TRSMMDot
TRSMMDot are a type of TRSWalkerObject. This are meant to be TRSWalkerObjects that have a minimap dot so TRSMMDot.Filter.MinimapDot is True by default and shouldn’t be changed. This also have a DotType variable for the type of ERSMinimapDot they have (PLAYER, NPC, ITEM) and a DotFilter which is used to filter mmdots in/out of circles and/or polygons so we only focus on the TRSMMDots we want.

TRSMMDot.Setup
procedure TRSMMDot.SetupEx(radius: Int32; shape: Vector3; coordinates: TPointArray); overload;
procedure TRSMMDot.Setup(radius: Int32; size, height: Double; coordinates: TPointArray); overload;
procedure TRSMMDot.Setup(radius: Int32; height: Double; coordinates: TPointArray); overload;
All this extend the basic TRSWalkerObject.Setup(coordinates: TPointArray) specifically for TRSMMDots. For TRSMMDots this are the methods that should be used for setting them up initially.

In TRSMMDot.Setup(radius: Int32; shape: Vector3; coordinates: TPointArray), radius is used to create a simple TRSDotFilterArray of that radius with cordinates and their center point. shape should be a vector3 of the target shape in number of tiles:

shape.X: Number of tiles of the target from west to east.

shape.Y: Number of tiles of the target from north to south.

shape.Z: Target height, this value has to be guessed, I recommend you try several values and debug it until it looks good to you. As some examples, player and npcs height is around 7, bank chests 4, yew/magic trees 14/16.

For NPCs that can move and are 1x2 tiles or any uneven number of tiles, I recommend you just set shape.X and shape.Y to the largest one. So a cow I would recommend making the shape 2x2.

The other methods all call this first one with certain default values:

Size makes shape.X and shape.Y equal to size.

If size is omited, shape.X and shape.Y are set to 1.

TRSMMDot._GetCuboids
function TRSMMDot._GetWMMCuboids(out mmTPA, dots: TPointArray; out dotFilters: TRSDotFilterArray): TCuboidExArray;
function TRSMMDot._GetMMCuboids(out dots: TPointArray): TCuboidExArray;
Internal helper TRSMMDot method used for debugging. You probably dont need to use this directly. You can see what this does in action by calling Debug(TRSMMDot).

TRSMMDot.GetCuboidArray
function TRSMMDot.GetCuboidArrayEx(out mmTPA, dots: TPointArray; out dotFilters: TRSDotFilterArray; out floorTiles: TRectArray; out roofTiles: TRectArray): TCuboidArray; overload;
function TRSMMDot.GetCuboidArray(): TCuboidArray; override;
Internal TRSMMDot method responsible for returning a TCuboidArray of our target on the 3D world (on mainscreen and outside of it). This uses the previous 2 helper methods to do this. You will probably never need to use this directly. You can visually see this in action by using the Debug() methods, this is responsible for the white lines surounding the targets.

TRSMMDot.FindEx
function TRSMMDot.FindEx(out mmPoints, dots: TPointArray; out DotFilters: TRSDotFilterArray; out floorTiles: TRectArray; out roofTiles: TRectArray; out cuboidArray: TCuboidArray; out atpa: T2DPointArray): Boolean;
TRSMMDot methods used to find a TRSMMDot. If found returns true, if not returns false. This “extended” method in particular is only meant for debugging and should be avoided outside of development/debugging. This is what is used when you call Debug(TRSMMDot).

TRSMMDot.Find
function TRSMMDot.Find(out atpa: T2DPointArray): Boolean; overload;
function TRSMMDot.Find(): Boolean; overload;
TRSMMDot methods used to find a TRSMMDot. If found returns true, if not returns false.

Example:

WriteLn RSNPCs.LumbridgeCook.Find(atpa); //Be in lumbridge castle and with a walker setup there.
Debug(atpa);
TRSMMDot._GetBaseRecord
function TRSMMDot._GetBaseRecord(): TRSMMDot;
Internal method used for casting custom TRSMMDots back to the base record.

TRSMMDot.Draw
procedure TRSMMDot.Draw(out bitmap: TMufasaBitmap);
Internal method used to draw found TRSMMDot in a TMufasaBitmap.

Example:

Bitmap.FromClient()
RSNPCs.LumbridgeCook.Draw(Bitmap); //Be in Lumbridge castle and with a walker setup there.
Bitmap.Debug();
Bitmap.Free();
TRSMMDot.SaveDebug
procedure TRSMMDot.SaveDebug();
Saves a debug image of the TRSMMDot to Simba\Screenshots\RSMMDots

Example:

RSNPCs.LumbridgeCook.SaveDebug(); //Be in Lumbridge castle and with a walker setup there.
TRSMMDot._UpdateTarget
procedure TRSMMDot._UpdateTarget(sender: PMouse; var x, y: Double; var done: Boolean);
Internal helper method of TMouseMovingEventEx type used to update the target position while the mouse is moving. You should probably not touch this if you don’t understand it.

TRSMMDot._HoverHelper
function TRSMMDot._HoverHelper(attempts: Int32; trackTarget: Boolean): Boolean;
Internal helper method used to hover a TRSMMDot target. You should not use this directly.

TRSMMDot._WalkHoverHelper
function TRSMMDot._WalkHoverHelper(attempts: Int32; trackTarget: Boolean): Boolean;
Internal helper method used to walk and hover a TRSMMDot target. You should not use this directly.

This is responsible for deciding wether we should walk to a TRSMMDot target or not before attempting to hover it.

TRSMMDot.Hover
function TRSMMDot.Hover(attempts: Int32 = 2; trackTarget: Boolean = TRACK_TARGET): Boolean;
Method used to hover a TRSMMDot target if it’s found on the mainscreen. It can update the target position as the mouse moves with trackTarget. For NPCs that move, this is highly recommended.

Example:

//Be in Lumbridge castle
RSW.WebWalk(WaspWeb.LOCATION_LUMBRIDGE);
RSNPCs.LumbridgeCook.Hover();
TRSMMDot.WalkHover
function TRSMMDot.WalkHover(attempts: Int32 = 2; trackTarget: Boolean = TRACK_TARGET): Boolean;
Method used to walk and hover a TRSMMDot target if it’s found on the mainscreen after walking. It can update the target position as the mouse moves with trackTarget. For NPCs that move, this is highly recommended.

Example:

//Be in Lumbridge castle
RSW.WebWalk(WaspWeb.LOCATION_LUMBRIDGE);
RSNPCs.LumbridgeCook.WalkHover();
TRSMMDot.Click
function TRSMMDot.Click(leftClick: Boolean = True; attempts: Int32 = 2): Boolean;
Method used to click a TRSMMDot target if it’s found on the mainscreen.

Example:

//Be in Lumbridge castle with a walker map of it loaded.
WriteLn RSNPCs.LumbridgeCook.Click();
TRSMMDot.SelectOption
function TRSMMDot.SelectOption(action: TStringArray; attempts: Int32 = 2): Boolean;
Method used to select an option on a TRSMMDot target if it’s found on the mainscreen.

Example:

//Be in Lumbridge castle with a walker map of it loaded.
WriteLn RSNPCs.LumbridgeCook.SelectOption(['Examine']);
TRSMMDot.WalkClick
function TRSMMDot.WalkClick(leftClick: Boolean = True; attempts: Int32 = 2): Boolean;
Method used to walk and click a TRSMMDot target if it’s found on the mainscreen.

Example:

//Be in Lumbridge castle with a walker map of it loaded.
WriteLn RSNPCs.LumbridgeCook.WalkClick();
TRSMMDot.WalkSelectOption
function TRSMMDot.WalkSelectOption(action: TStringArray; attempts: Int32 = 2): Boolean;
Method used to walk and select an option on a TRSMMDot target if it’s found on the mainscreen.

Example:

//Be in Lumbridge castle with a walker map of it loaded.
WriteLn RSNPCs.LumbridgeCook.WalkSelectOption(['Examine']);
type TRSNPC
TRSNPC are a type of TRSMMDot and TRSWalkerObject. This are meant to be TRSMMDot that have a yellow minimap dot so TRSNPC.Filter.MinimapDot is True by default and shouldn’t be changed.

type TRSGroundItem
TRSGroundItem are a type of TRSMMDot and TRSWalkerObject. This are meant to be TRSMMDot that have a red minimap dot so TRSGroundItem.Filter.MinimapDot is True by default and shouldn’t be changed.

type TRSPlayer
TRSPlayer are a type of TRSMMDot and TRSWalkerObject. This are meant to be TRSMMDot that have a white minimap dot so TRSPlayer.Filter.MinimapDot is True by default and shouldn’t be changed.

TRSMMDot.SetupUpText
procedure TRSNPC.SetupUpText(upText: TStringArray); override;
procedure TRSGroundItem.SetupUpText(upText: TStringArray); override;
procedure TRSPlayer.SetupUpText(upText: TStringArray); override;
Setup method that extends TRSWalkerObject.SetupUpText(upText: TStringArray); These are the methods that should be used to setup TRSNPCs, TRSGroundItems and TRSPlayers as it ensures that the TRSNPC.DotType is correctly set.

Debug
procedure Debug(rsobject: TRSObject); overload;
procedure Debug(mmdot: TRSMMDot); overload;
Methods used to debug TRSObjects and TRSMMDots.

Example:

Debug(RSObjects.GEBank); //Run in ge with a walker map setup there.

Debug(RSNPCs.LumbridgeCook); //Run in Lumbridge castle with a walker map setup there.