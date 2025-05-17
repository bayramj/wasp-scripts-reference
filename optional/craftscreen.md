CraftScreen
Methods to interact with the crafting screen on a furnace.

CraftScreen.IsOpen
function TRSCraftScreen.IsOpen(): Boolean;
function TRSCraftScreen.IsOpen(waitTime: Int32): Boolean;
Returns true if the gold crafting screen is visible. You can optionally specify a waitTime.

Example:

if CraftScreen.IsOpen() then
  CraftScreen.ClickItem(ERSCraftItem.GOLD_BRACELET, -1);
CraftScreen.Close
function TRSCraftScreen.Close(PressEscape: Boolean = False): Boolean;
Closes the gold crafting screen. Depending on PressEscape the function will either click the button or press backspace.

Example:

if CraftScreen.Close() then
  Writeln('Closed the gold crafting screen');
CraftScreen.SetQuantity
function TRSCraftScreen.SetQuantity(Amount: Int32): Boolean;
Sets the interface quantity to the set amount. Acceptable parameters include 1,5,10,X (custom amount) and -1 for ‘All’.

Example:

CraftScreen.SetQuantity(-1);
CraftScreen.CanCraftItem
function TRSCraftScreen.CanCraftItem(CraftItem: ERSCraftItem): Boolean;
Returns if the given ERSCraftItem can be crafted.

Example:

if CraftScreen.CanCraftItem(ERSCraftItem.RUBY_RING) then
  CraftScreen.ClickItem(ERSCraftItem.RUBY_RING, 5);
CraftScreen.IsItemHighlighted
function TRSCraftScreen.IsItemHighlighted(CraftItem: ERSCraftItem): Boolean;
Returns if the given ERSCraftItem is highlighted on the crafting interface.

Example:

if CraftScreen.IsItemHighlighted(ERSCraftItem.GOLD_BRACELET) then
  Keyboard.PressKey(VK_SPACE);
CraftScreen.CraftItem
function TRSCraftScreen.CraftItem(Item: TRSItem; Quantity: Int32; UseSpaceBar: Boolean=False): Boolean;
Sets the desired quantity then crafts the given ERSCraftItem on the gold crafting interface. If the item is highlighted (previously crafted) and UseSpaceBar is set to true, then the spacebar is used, if not then the interface item is clicked. Returns false if the given ERSCraftItem is not found on the interface.

Example:

if CraftScreen.CraftItem(ERSCraftItem.RUBY_AMULET, 5) then
  Writeln('Beginning crafting...');
