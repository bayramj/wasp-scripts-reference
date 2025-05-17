SilverScreen
Methods to interact with the silver screen on a furnace.

SilverScreen.IsOpen
function TRSSilverScreen.IsOpen(): Boolean;
function TRSSilverScreen.IsOpen(waitTime: Int32): Boolean;
Returns true if the silver crafting screen is visible. You can optionally specify a waitTime.

Example:

if SilverScreen.IsOpen() then
  SilverScreen.ClickItem('Unstrung symbol', -1);
SilverScreen.Close
function TRSSilverScreen.Close(PressEscape: Boolean = False): Boolean;
Closes the silver crafting screen. Depending on PressEscape the function will either click the button or press backspace.

Example:

if SilverScreen.Close() then
  Writeln('Closed the silver crafting screen');
SilverScreen.SetQuantity
function TRSSilverScreen.SetQuantity(Amount: Int32): Boolean;
Sets the interface quantity to the set amount. Acceptable parameters include 1,5,10,X (custom amount) and -1 for ‘All’.

Example:

SilverScreen.SetQuantity(-1);
SilverScreen.CanCraftItem
function TRSSilverScreen.CanCraftItem(Item: TRSItem; out ItemBox: TBox): Boolean;
Returns if the given TRSItem can be crafted. If so then a TBox of the disired item is returned.

Example:

if SilverScreen.CanCraftItem('Topaz bracelet', ItmBox) then
  Mouse.Move(ItmBox);
SilverScreen.IsItemHighlighted
function TRSSilverScreen.IsItemHighlighted(Item: TRSItem): Boolean;
Returns if the given TRSItem is highlighted on the silver crafting interface.

Example:

if SilverScreen.IsItemHighlighted('Unstrun symbol') then
  Keyboard.PressKey(VK_SPACE);
SilverScreen.CraftItem
function TRSSilverScreen.CraftItem(Item: TRSItem; Quantity: Int32; UseSpaceBar: Boolean=False): Boolean;
Sets the desired quantity then crafts on the given TRSItem on the silver screen interface. If the item is highlighted (previously crafted) and UseSpaceBar is set to true, then the spacebar is used, if not then the interface item is clicked. Returns false if ‘Item’ is not found on the interface.

Example:

if SilverScreen.CraftItem('Jade amulet (u)', 10) then
  Writeln('Beginning crafting...');
var SilverScreen
Global SilverScreen variable.
