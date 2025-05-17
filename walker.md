Walker
Extensions to SRL’s TRSWalker.

type TRSHeightMap
type
TRSHeightMap = record
  Disabled: Boolean;
  Map: TMufasaBitmap;
  MaxHeight: Double;
  MathCache: Double;
end;
TRSHeightMap is the type responsible for handling heights with walker when using WaspLib. This type does not need to be initiated as a variable and it’s meant to be used directly with it’s static methods.

Enabled is used to toggle the TRSHeightMap on/off. By default it will always be on unless there’s not a heightmap available for the map you load into walker. the heightmap MUST be named the same as the map you load with an “h” prepended. E.G.: hWorld.png

Map there’s not much to talk about this one, it’s simply the TMufasaBitmap loaded in the record.

MaxHeight This is what will be considered the max height possible in the calculations made by TRSHeightMap. There’s no way to accurately know what this should be, you should debug heights and set a value that looks good to you. Values might also vary between regions but I find 30 to be a fine value that works well in a lot of places if not all.

MathCache, not very important, simply a cache variable so we don’t repeat calculations when it’s not required.

TRSHeightMap.GetColor
function TRSHeightMap.GetColor(p: TPoint): Int64;
Returns the color of the heightmap at the specified point.

Example:

WriteLn TRSHeightMap.GetColor([100, 100]);
TRSHeightMap.DebugPosition
procedure TRSHeightMap.DebugPosition(p: TPoint);
Debug a point in the loaded heightmap.

Example:

TRSHeightMap.DebugPosition(RSW.GetMyPos());
TRSWalkerMap.Load
procedure TRSWalkerMap.Load(fileName: String; Scaling: Integer); override;
procedure TRSWalkerMap.Load(fileName: String; aRegions: TBoxArray; Scaling: Integer; Padding: Integer = 50); override;
procedure TRSWalkerMap.Load(fileName: String; aRegion: TBox; scaling: Integer; padding: Integer = 50); override;
procedure TRSWalkerMap.Load(fileName: String; start: TPoint; scaling: Int32; out aRegion: TBox; padding: Int32 = 50); override;
Overrides SRL’s TRSWalkerMap.Load() so it loads the respective heightmap if it exists. This is an internal Walker method, you probably don’t need to call it.

Walker.InternalSetup
procedure TRSWalker.InternalSetup(); override;
Overrides SRL’s Walker.InternalSetup() so it uses WaspWeb as the walker webgraph and so it uses ScreenWalk by default. This is an internal Walker method, you probably don’t need to call it. It also sets up the ScriptWalker pointer which is used for several things in WaspLib like TRSWalkerObjects and Skunk’s transport system.

Walker.SetupNamedRegion
procedure TRSWalker.SetupNamedRegion(region: TRSBankRegion = []); overload;
Use this if you want to setup a walker with whatever the user has setup in WLSettings.BankLocation. You can optionally pass in your own region but it’s really meant to use the default.

Example:

WLSettings.BankLocation := EWLBankLocation.CASTLE_WARS_BANK;
Walker.SetupNamedRegion();
Walker.Map.Map.Debug();
Walker.GetHeight
function TRSWalker.GetHeight(p: TPoint = []; global: Boolean = True): Double;
Returns the height of the player at the specified coordinate with the help of TRSHeightMap. If p is [], which is the default then we will use our current position. global decides wether the coordinate is converted to global coordinates or internal walker coordinates (read about walker regions for more info).

Example:

WriteLn rsw.GetHeight();
Walker.DebugHeightTiles
procedure TRSWalker.DebugHeightTiles(angle: Double = -1);
Displays a debug image of the tiles visible on the mainscreen with their height adjusted according to the TRSHeightMap. This is very useful if you need to adjust TRSHeightMap.MaxHeight.

Example:

rsw.DebugHeightTiles();
Walker.GetMyPos
function TRSWalker.GetMyPos(out height: Double): TPoint; overload;
Overload that also returns the player height.

Example:

WriteLn RSW.GetMyPos(height);
WriteLn height;
Walker.GetHeightDiff
function TRSWalker.GetHeightDiff(p: TPoint): Double;
function TRSWalker.GetHeightDiff(p, q: TPoint): Double; overload;
Returns the height difference between 2 points. If only one point is passed, the player position is used as one of them.

Example:

WriteLn RSW.GetMyPos(RSW.GetMyPos(), [100, 100]);
TRSWalker.AtTile
function TRSWalker.AtTile(worldPoint: TPoint; Distance: Int32 = 4): Boolean;
function TRSWalker.AtTile(worldPointArray: TPointArray; Distance: Int32 = 4): Boolean; overload;
method used to quickly check if we are within distance of a certain worldPoint. This distance is measure in pixels and in a radial way. You can optionally pass in a TPA to check if the closest point is within distance.

This is a TRSWalker method so it will exist both on TRSWalker and TRSWalker.

TRSWalker.GetClosestPoint
function TRSWalker.GetClosestPoint(worldPointArray: TPointArray): TPoint;
method used to get the closest Point to the Player out of a TPA.

This is a TRSWalker method so it will exist both on TRSWalker and TRSWalker.

TRSWalker.WebWalk
function TRSWalker.WebWalk(destinations: TPointArray; waitUntilDistance: Int32 = 0; pathRandomness: Double = 0): Boolean; overload;
method used to webwalk to the closest Point to the player. An example use case is for example, if you have sevel bank booths you can use, those would be your Destination TPA. You will likely want to use the closest bank booth to you, so you use this.

This is a TRSWalker method so it will exist both on TRSWalker and TRSWalker.

TRSWalker.WorldToMM
function TRSWalker.WorldToMM(me: TPoint; tpa: TPointArray; radians: Double): TPointArray; overload;
function TRSWalker.WorldToMM(tpa: TPointArray): TPointArray; overload;
function TRSWalker.WorldToMM(me: TPoint; atpa: T2DPointArray; radians: Double): T2DPointArray; overload;
function TRSWalker.WorldToMM(atpa: T2DPointArray): TPointArray; overload;
function TRSWalker.WorldToMM(me: TPoint; dotFilter: TRSDotFilter; roll: Double = $FFFF): TRSDotFilter; overload;
function TRSWalker.WorldToMM(dotFilterArray: TRSDotFilterArray; roll: Double = $FFFF): TRSDotFilterArray; overload;
Overloaded methods required for ATPAs and TRSDotFilters. For more information on TRSDotFilter check their documentation.

This is a TRSWalker method so it will exist both on TRSWalker and TRSWalker.

TRSWalker.MakePointVisible
function TRSWalker.MakePointVisible(p: TPoint): Boolean;
function TRSWalker.MakePointVisible(tpa: TPointArray): Boolean; overload;
Wrapper function used to attempt to make a Point visible on the MainScreen.

This are TRSWalker methods so they will exist both on TRSWalker and TRSWalker.

TRSWalker.GetCuboidMS
function TRSWalker.GetCuboidMS(me, loc: TPoint; tile: Vector3 = [1, 1, 4]; Offset: Vector2 = [0, 0]): TPointArray;
function TRSWalker.GetCuboidMS(loc: TPoint; tile: Vector3 = [1, 1, 4]; Offset: Vector2 = [0, 0]): TPointArray; overload;
This are TRSWalker methods so they will exist both on TRSWalker and TRSWalker.

To understand what this does, you should read about TRSMinimap.GetTileMS() and TPointArray.ConvexHull() and understand what they do. This calls TRSMinimap.GetCuboidMS() internally which in turn will use both methods above.

To put it simply, this will will first calculate a floor rectangle with tile.Z, or height if you prefer of 0 and then calculate the top rectangle of the tile.Z you specified.

After this 2 rectangles are calculated a polygon is then made out of the two, resulting in a ConvexHull which is returned.

This is perfect to to get an accurate bounding polygon of objects and NPCs which you can use to accurately color search after.

The example below will show you how it could be used to retrieve an accurate player bounding polygon:

Example:

Debug(RSW.GetCuboidMS([100, 100], [1, 1, 4], Offset));     //This will draw a polygon around the coordinate [100, 100].
TRSWalker.GetTileArrayMS
function TRSWalker.GetTileArrayMS(me: TPoint; locArray: TPointArray; tile: Vector3 = [1, 1, 0]; Offset: Vector2 = [0, 0]): TRectArray;
function TRSWalker.GetTileArrayMS(locArray: TPointArray; tile: Vector3 = [1, 1, 0]; Offset: Vector2 = [0, 0]): TRectArray; overload;
This are wrapper functions to retrieve multiple tiles. Refer to SRL’s TRSWalker.GetTileMSEx() and TRSWalker.GetTileMS() for more information.

This are TRSWalker methods so they will exist both on TRSWalker and TRSWalker.

TRSWalker.GetCuboidArrayMS
function TRSWalker.GetCuboidArrayMS(me: TPoint; locArray: TPointArray; tile: Vector3 = [1, 1, 4]; Offset: Vector2 = [0, 0]): T2DPointArray;
function TRSWalker.GetCuboidArrayMS(locArray: TPointArray; tile: Vector3 = [1, 1, 4]; Offset: Vector2 = [0, 0]): T2DPointArray;
Gives you an array of mainscreen polygons. Read Minimap.GetCuboidMS for more information.

This are TRSWalker methods so they will exist both on TRSWalker and TRSWalker.

Example:

TPA := Minimap.GetDots(ERSMinimapDot.Player);   //find all player dots and returns their coodinates.
Debug(Minimap.GetCuboidArrayMS(TPA, [2, 3, 5], [2, 2])); //This will draw a polygon that is 2 by 3 tiles and height 5 in the mainscreen where each NPC is.
TRSWalker.GetMSPolygon
function TRSWalker.GetMSPolygon(tpa: TPointArray): TPointArray;
function TRSWalker.GetMSPolygonArray(atpa: T2DPointArray): T2DPointArray;
This function converts a list of points to their respective points in the minimap. This is extremely useful if you want to be sure you are within an area. To make a polygon or a polygon array easily you can use Simba/Includes/WaspLib/tools/walkerpolygon.simba.

This are TRSWalker methods so they will exist both on TRSWalker and TRSWalker.

Example:

Debug(RSW.GetMMPoly(TPA).Connect());    //This will draw your TPA on the minimap.
TRSWalker.InPoly
function TRSWalker.InPoly(locArray: TPointArray): Boolean;
Checks if you are inside a polygon. If you need to debug the polygon check the example in TRSWalker.GetMMPoly.

This are TRSWalker methods so they will exist both on TRSWalker and TRSWalker.