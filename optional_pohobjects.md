POH Objects
The following methods are related to interacting with POH Handler TRoomObject.

POH.Find
function TRSPOHHandler.FindEx(objType: ERSRoomObject; out cuboids: TCuboidExArray; out atpa: T2DPointArray):
function TRSPOHHandler.FindAny(objType: ERSRoomObject; out tpa: TPointArray): Boolean;
function TRSPOHHandler.FindAll(objType: ERSRoomObject; out atpa: T2DPointArray): Boolean;
Method used to find a TRoomObject by specifying a ERSRoomObject. You can find any occurence of the object or all of them depending on the method you use. The extended version of the method is mostly for debugging.

TRSPOHHandler.Draw()
procedure TRSPOHHandler.Draw(out bitmap: TMufasaBitmap; objType: ERSRoomObject);
Internal method used to draw found TRoomObject in a TMufasaBitmap. An easy way to see this in action is to use Debug(ERSRoomObject).

POH.Interact
function TRSPOHHandler.Hover(objType: ERSRoomObject): Boolean;
function TRSPOHHandler.Click(objType: ERSRoomObject): Boolean;
function TRSPOHHandler.Select(objType: ERSRoomObject; options: TStringArray): Boolean;
Method used to interact with a TRoomObject by specifying a ERSRoomObject. The interactions are self explanatory.

Example:

POH.Setup(); //call from the northwest tile of your exit portal.
WriteLn POH.Hover(ERSRoomObject.POOL); //pool has to be on the same room, north, west, south or east.
POH.WalkInteract
function TRSPOHHandler.WalkHover(objType: ERSRoomObject; attempts: Int32): Boolean;
function TRSPOHHandler.WalkClick(objType: ERSRoomObject; attempts: Int32): Boolean;
function TRSPOHHandler.WalkSelect(objType: ERSRoomObject; options: TStringArray; attempts: Int32): Boolean;
Method used to walk and interact with a TRoomObject by specifying a ERSRoomObject. The interactions are self explanatory.

Example:

POH.Setup(); //call from the northwest tile of your exit portal.
WriteLn POH.Hover(ERSRoomObject.POOL); //pool has to be on the same room, north, west, south or east.
var POH
var POH
Global variable to use the type TRSPOHHandler.

Debug
procedure Debug(pohObject: ERSRoomObject); overload;
Method used to debug TRoomObject.