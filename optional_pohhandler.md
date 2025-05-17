POH Handler
The POH Handler is a handler responsible for making sense of a player’s POH (Player Owned House) without knowing any info about it’s setup in advance.

Note 



Several rooms in a POH are unique on the minimap, with windows and/or doors of several sizes and different places. By having this rooms saved in the following format:

_images/poh.png
Most relevant rooms for a POH stripped of their floor colors

We can attempt to match what we have on the minimap to those rooms and slowly build a map of the POH.

Some rooms share the same room layout or are very similar to others and for those we use some mainscreen information to make up what the room is, e.g., Nexus room, Combat Hall and Quest Hall are all identical.

PRSWalker
TRSWalker pointer.

type TRSPOHHandler
type
  TRSPOHHandler = record
    Map: TPOHMap;
    RoomObjects: array [ERSRoomObject] of TRoomObject;
    EnableRunAtEnergy: Int32;
    Similarity: Double;
  end;
The core record used to handle navigating a POH.

POH.Init()
procedure TRSPOHHandler.Init();
Internal method automatically called for your on script startup along with SRL.Setup(). You do not have to call it yourself.

POH.GetAdjacentRooms()
function TRSPOHHandler.GetAdjacentRooms(p: TPoint): TPointArray; static;
Helper static method that returns coordinates that belong to the north, west, south and east rooms of the point passed in. This assumes the compass is set to 0 (North) or that you’ve rotated your coordinates so the math works as if you had the compass set that way. Ideally, you will want to pass in a room top left corner to this to get the top left corner of each adjacent room.

TRSPOHHandler.GetRoomCoordinate()
function TRSPOHHandler.GetRoomCoordinate(topLeft, p: TPoint; angle: Double; rotation: Int32): TPoint; static;
Helper static method that converts a room point p (which is always between [0,0] and [32,32] to a point on the minimap. Optionally the point can be rotated on the room’s center in 90º increments which is decided by rotation. For example, if rotation is 3, the point will be rotated 90*3=270º on the room’s center.

This is useful to look for mainscreen objects in a room we don’t know the rotation, we can brute force all the possible rotations and look for what we want.

POH.GetCuboid()
function TRSPOHHandler.GetCuboid(topLeft, p: TPoint; tile: Vector3; angle: Double; rotation: Int32): TCuboidEx; static;
Static mehod that returns a TCuboidEx on the mainscreen of a point we specify p with a given rotation on the room’s center. TRSPOHHandler.GetRoomCoordinate() is used to get the minimap point which then uses Minimap.GetCuboidMS() to give us a cuboid as a result.

To work, this requires the room’s topLeft TPoint and the compass angle.

POH.ContainsObject()
function TRSPOHHandler.ContainsObject(objType: ERSRoomObject; topLeft: TPoint; angle: Double; rotation: Int32): Boolean;
Checks if a TRoomObject stored in POH.RoomObjects exists in a room at a given rotation.

POH.MapRoomObjects()
procedure TRSPOHHandler.MapRoomObjects(room: ERSHouseRoom; topLeft: TPoint; roomIndex: TPoint; angle: Double);
Method responsible for mapping known TRoomObjectTRoomObject coordinates which later can be used to interact with them.

POH.MapAdjacentRooms()
procedure TRSPOHHandler.MapAdjacentRooms(minimapBMP: TMufasaBitmap; topLeft, currentRoom: TPoint; angle: Double);
The core of the “POH Handler”. This method is what’s responsible for mapping unknown adjacent rooms (north, west, south and east). If you know what you are doing you can call this directly, but this is called automatically by POH.Position() and POH.Setup().

POH.Setup()
procedure TRSPOHHandler.Setup();
The method that sets up the “POH Handler” so it can be used. It’s your responsibility to call it and it must be called from your POH entrance. There is some wiggle room as from where you can use this on your garden and you might get away using it from anywhere but for best results you should use this from the tile right northwest to your exit portal. This is the tile that the POH.Setup() assumes you will be calling it from and it’s the tile you will always be in as soon as you enter your POH no matter the method you choose to enter it (teleport, using the portal, building or non building mode, …).

Example:

if MainScreen.WaitLoadingPOH(5000) then
  POH.Setup();
POH.LoadSuroundings()
procedure TRSPOHHandler.LoadSuroundings(minimapBMP: TMufasaBitmap; p: TPoint; angle: double);
Wrapper method that performs some common math required by POH.MapAdjacentRooms(). You can use this directly if you know what you are doing, but this is called automatically for you with POH.Position().

POH.Position()
function TRSPOHHandler.Position(): TPoint;
Returns the player position relative to the POH.Map. Whenever this method is called, if there’s unknown adjacent rooms (north, west, south and east), they will be mapped.

POH.DebugPosition()
procedure TRSPOHHandler.DebugPos();
Debugs the current player position on the POH.Map.

Example:

{$I WaspLib/optional/handlers/poh.simba}
begin
  POH.Setup(); //call from the northwest tile of your exit portal.
  while True do
    POH.DebugPos();
end;
POH.GetCurrentRoom()
function TRSPOHHandler.GetCurrentRoom(): ERSHouseRoom;
Returns the current type ERSHouseRoom we are on.

Example:

POH.Setup(); //call from the northwest tile of your exit portal.
WriteLn POH.GetCurrentRoom();