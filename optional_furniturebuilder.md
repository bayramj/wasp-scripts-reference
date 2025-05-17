FurnitureBuilder
Methods to interact with the FurnitureBuilder interface.

UNFINISHED! AND NOT WORKING!

FurnitureBuilder.IsOpen
function TRSFurnitureBuilder.IsOpen(WaitForItems: Boolean = True): Boolean;
Returns true if the FurnitureBuilder is visible.

WaitForItems determines if the method waits 1-2 seconds items to load as there can be a small delay before items are visible.

FurnitureBuilder.Setup
procedure FurnitureBuilder.Setup;
Initializes FurnitureBuilder variables.

Note

This is automatically called on the FurnitureBuilder variable.

FurnitureBuilder.Close
function TRSFurnitureBuilder.Close(UseKeyboard: Boolean = False): Boolean;
Closes the furniture builder, Depending on UseKeyboard the function will either click the button or press backspace.

Example:

 WriteLn FurnitureBuilder.Close();
var FurnitureBuilder
Global FurnitureBuilder variable.

