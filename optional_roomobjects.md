RoomObjects
File responsible for handling house objects. Similar to type TRSObject but exclusive to the POH.

ERSRoomObject
ERSRoomObject = (POOL, FAIRY_TREE, JEWELLERY_BOX, PRAYER_ALTAR, MAGIC_ALTAR, LARDER, LECTERN, MYTH_CAPE, NEXUS, PORTAL);
TRoomObject
TRoomObject = record
  Coordinates: TPointArray;
  Shape: Vector3;
  UpText: TStringArray;
  Finder: TRSObjectFinder;
  RoomOffset: TPoint;
end;
Record used to store and interact information about POH room objects.

TRoomObject.Init()
procedure TRoomObject.Init(upText: TStringArray; shape: Vector3; roomOffset: TPoint);
This method sets up some basic info about a TRoomObject.

TRoomObject.Setup()
procedure TRoomObject.Setup(obj: ERSRoomObject); overload;
Basically the same as TRoomObject.Init() with some already known information.

Example:

var
  obj: TRoomObject;
begin
  obj.Setup(ERSRoomObject.POOL);
end;
TRoomObject.AddCoordinates()
procedure TRoomObject.AddCoordinates(coordinates: TPointArray);
Adds coordinates to a TRoomObject. Can be called multiple times to add more coordinates.

Example:

var
  obj: TRoomObject;
begin
  obj.Setup(ERSRoomObject.POOL);
  obj.AddCoordinates([[50, 50]]);
end;
TRoomObject.Find
function TRoomObject.FindEx(mmPoints: TPointArray; radians: Double; out cuboids: TCuboidExArray; out atpa: T2DPointArray; stopAfter: Int32 = 0): Boolean;
function TRoomObject.FindAny(mmPoints: TPointArray; radians: Double; out atpa: T2DPointArray): Boolean;
function TRoomObject.FindAll(mmPoints: TPointArray; radians: Double; out atpa: T2DPointArray): Boolean;
Find a TRoomObject. You may choose to find any occurence of the object or all available. The extended version of the method is mostly for debugging.

TRoomObject.Draw
procedure TRoomObject.Draw(out bitmap: TMufasaBitmap; mmPoints: TPointArray; radians: Double);
Internal method used to draw found TRoomObject in a TMufasaBitmap.

TRoomObject.Interact
function TRoomObject.Hover(mmPoints: TPointArray; radians: Double): Boolean;
function TRoomObject.Click(mmPoints: TPointArray; radians: Double): Boolean;
function TRoomObject.Select(options: TStringArray; mmPoints: TPointArray; radians: Double): Boolean;
Interacts with a TRoomObject. The interaction type is self explanatory.