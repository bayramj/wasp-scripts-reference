Items Extensions
This file contains useful methods to extend the TRSItem and allow things like ‘Prayer potion(1..4)’ to be used.

TRSItem.Reorder
function TRSItem.Reorder(LowToHi: Boolean = True): TRSItem;
Used to retrieve reordered items. Items that have several “doses” or “portions” like a Saradomin brew (1..4) might need to be reordered sometimes.

When we want to consume them, we usually want to prioritize lower dosage items to get inventory space. However when we are withdrawing it from the bank, we want to prioritize the highest dosage items to maximize trips length.

This function reorders depending on what you set in LowToHi. By default it reorders items from low to high.

TRSItem.GetPortions
function TRSItem.GetPortions(): Int32;
Get the amount of portions in the multi dose item (an item with “(x..z)”).

TRSItem.GetPortion
function TRSItem.GetPortion(): Int32;
Get the portion number of one specific Item.

Example:

Item := 'Saradomin brew(4)';

WriteLn Item.GetPortion; //This will print 4.
Item.GetArray
function TRSItem.GetArray(): TRSItemArray;
Used to retrieve an item array of our multi dose/portion item.

Example:

var
  Item: TRSItem;
begin
  Item := 'Saradomin brew(1..4)';

  WriteLn Item.GetArray();
  //This will print: ['Saradomin brew(1)', 'Saradomin brew(2)', 'Saradomin brew(3)', 'Saradomin brew(4)']
end;
Item.GetSingle
function TRSItem.GetSingle(Lo: Boolean = True): TRSItem;
Used to retrieve the lowest or highest dose of our multi dose/portion item.

Example:

var
  Item: TRSItem;
begin
  Item := 'Saradomin brew(1..4)';

  WriteLn Item.GetSingle(True); //This will print: 'Saradomin brew(1)'
end;