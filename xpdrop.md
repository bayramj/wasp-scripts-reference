XPDrop
Methods to interact with the XP Drops.

const XP_COLORS
XP_COLORS is the constant holding all possible XPDrop colors.

XP_COLORS: TIntegerArray = [$FFFFFF, $FFC8C8, $FF00FF, $C8FFC8, $64FF64, $40FFFF, $1F98FF, $C8C8FF];
XPDrop.Setup
procedure TRSXPDrop.Setup;
Setups the XPDrop.

Note

This is automatically called on the XPDrop variable.

XPDrop.IsOpen
function TRSXPDrop.IsOpen: Boolean;
Returns true if the XP Drops are on.

XPDrop.Open
function TRSXPDrop.Open: Boolean;
Attempts to open the XP Drops if they are closed.

XPDrop._Find
function TRSXPDrop._Find: Boolean;
Internal function to find XPDrops. Searches for all colors in XP_COLORS within the current XPDrops location.

XPDrop.UpdateLocation
function TRSXPDrop.UpdateLocation: Boolean;
Internal function to update XPDrops location.

XPDrop.FindDrop
function TRSXPDrop.FindDrop: Boolean;
Returns true if a XPDrop is found.

Example:

 WriteLn XPDrop.FindDrop;
XPDrop.WaitDrop
function TRSXPDrop.WaitDrop: Boolean;
Waits WaitTime until an XPDrop is found.

Example:

 WriteLn XPDrop.WaitDrop(1000);
var XPDrop
Global XPDrop variable.