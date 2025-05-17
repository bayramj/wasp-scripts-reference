POHMap
The POH Map is what’s responsible for mapping a user’s POH.

type ERSHouseRoom
ERSHouseRoom = (
  UNKNOWN, GARDEN, SUPERIOR_GARDEN, MENAGERIE_OPEN, MENAGERIE_CLOSED,
  STUDY_PARLOUR, KITCHEN_BEDROOM, ACHIEVEMENT_GALLERY, QUEST_NEXUS, COMBAT,
  COSTUME, ALTAR, PORTAL, WORKSHOP
);
type TPOHMap
type
  TPOHMap = record
    AMOUNT, SIZE: Int32;
    Map: TMufasaBitmap;
    Rooms: array of array of ERSHouseRoom;
    RoomsMap: TMufasaBitmap;
    ERoomBitmaps: array [ERSHouseRoom] of TMufasaBitmap;
    GrassColor: Int32;
  end;
Helper record used by the type TRSPOHHandler. All TPOHMap methods are helper methods for the type TRSPOHHandler and you shouldn’t have to call them for anything.

TPOHMap.Free()
procedure TPOHMap.Free();
Internal method automatically called for your on script termination. You do not have to call it yourself.

TPOHMap.Init()
procedure TPOHMap.Init(size, amount: Int32);
Internal method automatically called for your on script startup along with POH.Init(). You do not have to call it yourself.

TPOHMap.GetRoomBitmapBox()
function TPOHMap.GetRoomBitmapBox(room: ERSHouseRoom): TBox;
Internal method used to get the box of the type ERSHouseRoom you pass in.

This box is a box of the following image:

poh rooms

Example:

{$I WaspLib/optional/handlers/poh.simba}
begin
  WriteLn POH.Map.GetRoomBitmapBox(ERSHouseRoom.SUPERIOR_GARDEN);
end;
TPOHMap.GetRoomBitmap()
function TPOHMap.GetRoomBitmap(room: ERSHouseRoom; color: Int32 = -1): TMufasaBitmap;
Internal method used to retrieve a bitmap of the type ERSHouseRoom you pass in.

Example:

{$I WaspLib/optional/handlers/poh.simba}
var
  bmp: TMufasaBitmap;
begin
  bmp := POH.Map.GetRoomBitmap(ERSHouseRoom.SUPERIOR_GARDEN);
  bmp.Debug();
  bmp.Free();
end;
TPOHMap.RotateBitmap()
function TPOHMap.RotateBitmap(bitmap: TMufasaBitmap; rotation: Int32): TMufasaBitmap; static;
Rotates a bitmap by 90º increments a rotation number of times. This was made specifically for room bitmaps, but you could use it for other stuff I guess. It’s also a static method and can be called directly from the type.

Example:

{$I WaspLib/optional/handlers/poh.simba}
var
  bmp: TMufasaBitmap;
begin
  bmp := POH.Map.GetRoomBitmap(ERSHouseRoom.MENAGERIE_OPEN);
  bmp.Debug();
  Wait(2000);
  TPOHMap.RotateBitmap(bmp, 1);
  bmp.Debug();
  bmp.Free();
end;
TPOHMap.WriteRoom()
procedure TPOHMap.WriteRoom(room: ERSHouseRoom; index: TPoint);
Internal method used to write a room to TPOHMap.Rooms cache. This uses an TPoint as a room index in a 2D array of type ERSHouseRoom.

Unless you know what you are doing, you definitly should not use this for anything.

Example:

POH.Map.WriteRoom(ERSHouseRoom.SUPERIOR_GARDEN, [3,3]);
TPOHMap.ReadRoom()
function TPOHMap.ReadRoom(index: TPoint): ERSHouseRoom;
Internal method used to read a cached room in TPOHMap.Rooms. This uses an TPoint as a room index.

Unless you know what you are doing, you don’t need this, but there’s no harm in using it.

Example:

WriteLn POH.Map.ReadRoom([3,3]);
TPOHMap.PrintRooms()
procedure TPOHMap.PrintRooms();
Debugging helper method used to read a cached rooms in TPOHMap.Rooms. This will print the whole cache nicely formated in a way that is human friendly like you were looking at the house map.

Unless you know what you are doing, you don’t need this, but there’s no harm in using it.

Note 


Example:

POH.Setup();
POH.Map.PrintRooms();
TPOHMap.DrawMap()
procedure TPOHMap.DrawMap(bmp: TMufasaBitmap; room: ERSHouseRoom; p: TPoint);
procedure TPOHMap.DrawMap(room: ERSHouseRoom; color: Int32; p: TPoint); overload;
Methods used to draw the POH map and cache the rooms drawn in TPOHMap.Rooms.

Example:

POH.Map.DrawMap(ERSHouseRoom.SUPERIOR_GARDEN, POH.GrassColor, [3,3]);
POH.Map.Debug();
POH.Map.PrintRooms();
TPOHMap.GetPointIndex()
function TPOHMap.GetPointIndex(p: TPoint): TPoint;
Helper method that converts a normal TPoint to a index used by TPOHMap.ReadRoom().

Example:

WriteLn POH.Map.GetPointIndex(POH.GetPos());
TPOHMap.GetRoom()
function TPOHMap.GetRoom(p: TPoint): ERSHouseRoom;
Helper method that returns the cached room in TPOHMap.Roomswith the help of TPOHMap.GetPointIndex() and TPOHMap.ReadRoom().

Example:

WriteLn POH.Map.GetRoom(POH.GetPos());
TPOHMap.GetRoomTopLeft()
function TPOHMap.GetRoomTopLeft(p: TPoint): TPoint;
Helper method that returns the top left point of a mapped room that the specified p belongs to. This is required to do accurate “room math”.

Example:

WriteLn POH.Map.GetRoomTopLeft(POH.GetPos());
TPOHMap.GetAdjacentIndices()
function TPOHMap.GetAdjacentIndices(index: TPoint): TPointArray; static;
Helper method that returns indices of the adjacent rooms (north, west, south and east) on the TPOHMap.Rooms cache. It’s also a static method and can be called directly from the type.

Example:

WriteLn TPOHMap.GetAdjacentIndices([3,3]);
TPOHMap.SampleSearch()
function TPOHMap.SampleSearch(minimapBMP: TMufasaBitmap; sampleSize: Int32 = 50; sampleAmount: Int32 = 3): TPoint;
Helper method that returns the the position of the minimapBMP in the TPOHMap.Map, essentially getting the player position.

Example:

{$I WaspLib/optional/handlers/poh.simba}
var
  minimapBMP: TMufasaBitmap;
begin
  minimapBMP := TRSPOHHandler.GetCleanMinimap();
  minimapBMP.ReplaceColor(1, POH.Map.GrassColor);
  WriteLn POH.Map.SampleSearch(minimapBMP, SAMPLE_SIZE);
  minimapBMP.Free();
end;