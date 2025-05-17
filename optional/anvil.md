Anvil
Anvil interface.

Anvil.GetSlots
function TRSAnvil.GetSlots: TBoxArray;
Returns the all available anvil slots.

Example:

Debug(Anvil.GetSlots());
Anvil.Setup
procedure Anvil.Setup;
Initializes Anvil variables.

Note

This is automatically called on the Anvil variable.

Anvil.IsOpen
function TRSAnvil.IsOpen(): Boolean;
function TRSAnvil.IsOpen(waitTime: Int32; interval: Int32 = -1): Boolean; overload;
Returns true/false whether the anvil interface is open or not.

Example:

 WriteLn Anvil.IsOpen();
Anvil.Close
function TRSAnvil.Close(pressEscape: Boolean): Boolean;
function TRSAnvil.Close(chance: Double = BioHash): Boolean; overload;
Closes the anvil interface, depending on pressEscape the function will either click the button or press escape.

Example:

 WriteLn Anvil.Close;
var Anvil
Global Anvil variable.
