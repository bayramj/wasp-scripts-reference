Minimap to MainScreen
Methods to handle MM2MS (Minimap to MainScreen). Extends SRL’s MM2MS.

type TRSMainScreenShape
This record holds information about the shape of a TRSWalkerObject and it’s rotation.

TRSMainScreenShape.Shape has 3 values, X, Y and Z. X and Y are how wide a object is, measured in game tiles. Z is the object height which has to be guessed and tested for a good value.

For example, a bank chest would be roughly [1, 1, 4]. A bank booth would be roughly [1, 1, 8].

Angle is used to rotate an object and should be done in radians.

Minimap.GetCuboidMS
function TRSMinimap.GetCuboidMSEx(loc: TPoint; shape: TRSMainScreenShape; startHeight: Double = 0; offset: Vector2 = [0, 0]; angle: Single = $FFFF): TCuboidEx;
function TRSMinimap.GetCuboidMS(loc: TPoint; shape: TRSMainScreenShape; offset: Vector2 = [0, 0]; angle: Single = $FFFF): TCuboidEx;
function TRSMinimap.GetCuboidArrayMSEx(locArray: TPointArray; shapeArray: TRSMainScreenShapeArray; startHeights: TDoubleArray; offset: Vector2 = [0, 0]; angle: Single = $FFFF): TCuboidExArray;
function TRSMinimap.GetCuboidArrayMS(locArray: TPointArray; shapeArray: TRSMainScreenShapeArray; offset: Vector2 = [0, 0]; angle: Single = $FFFF): TCuboidExArray
function TRSMinimap.GetCuboidArrayMS(locArray: TPointArray; shape: TRSMainScreenShape; offset: Vector2 = [0, 0]; angle: Single = $FFFF): TCuboidExArray; overload;
Converts minimap coordinates to mainscreen cuboid(s) at a specific height. To understand what this better, you should read about Minimap.GetTileMS and TPointArray.ConvexHull and understand what they do.

To put it simply, this will will first calculate a floor rectangle with tile.Z, or height if you prefer of 0 and then calculate the top rectangle of the tile.Z you specified.

After this 2 rectangles are calculated, a cuboid is then made out of the two, resulting in a ConvexHull which is returned.

This is perfect to to get an accurate bounding cuboid of objects and NPCs which you can use to accurately color search after.

Note 


The example below will show you how it could be used to retrieve an accurate player bounding cuboid.

Example:

P := Minimap.GetDots(ERSMinimapDot.PLAYER)[0];         //find a player dot and returns it's coodinates.
offset := [2 , 2];                                     //Minimap dots are actually returned with a slight offset of -2, -2 when converting them to the mainscreen.
Debug(Minimap.GetCuboidMS(P, [1, 1, 7], offset));     //This will draw a polygon around the nearest player.
MM2MS.SetupZoom
procedure TMM2MS.SetupZoom;
Wrapper procedure to easily setup MM2MS.ZoomLevel.

Example:

MM2MS.SetupZoom;
WriteLn MM2MS.ZoomLevel;
Minimap.GetFaceablePoints
function TRSMinimap.GetFaceablePoints(): TPointArray;
Gives the center point of the 8 tiles that are directly close to the player. This are the tiles the player can “face”.

Minimap.GetCardinalPoints
function TRSMinimap.GetCardinalPoints(): TPointArray;
Gives the center point of the 4 cardinal points (North, West, South and East) that are directly close to the player. This are the tiles the player can “face”.

