DriftNet
DriftNet interface by Reldnahc.

TRSDriftNet.BankOverlayOpen
function TRSDriftNet.BankOverlayOpen(): Boolean;
Returns True if the bank loot overlay is activated

Example:

if DriftNet.BankOverlayOpen() then
  Driftnet.GetButton(ERSDriftNetButton.OVERLAY_CONFIRM).Click();
TRSDriftNet.DestroyOverlayOpen
function TRSDriftNet.DestroyOverlayOpen(): Boolean;
Returns True if the destroy loot overlay is activated

Example:

if DriftNet.DestroyOverlayOpen() then
  Driftnet.GetButton(ERSDriftNetButton.OVERLAY_CANCEL).Click();
TRSDriftNet.HasOverlay
function TRSDriftNet.HasOverlay(): Boolean;
Returns True if either overlay is activated

Example:

if DriftNet.HasOverlay() then
  Driftnet.GetButton(ERSDriftNetButton.OVERLAY_CONFIRM).Click();
TRSDriftNet.GetSlotBoxes
function TRSDriftNet.GetSlotBoxes(): TBoxArray;
Returns a TBoxArray containing each item slot

TRSDriftNet.GetButtons
function TRSDriftNet.GetButtons(): TRSButtonArray;
Returns a TRSButtonArray containing the avaiable buttons. Changes depending on if there is an overlay.

TRSDriftNet.GetButton
function TRSDriftNet.GetButton(): TRSButton;
Returns a specific button if its available

Example:

if not DriftNet.HasOverlay() then
  Driftnet.GetButton(ERSDriftNetButton.BANK_ALL).Click();
if DriftNet.BankOverlayOpen() then
  Driftnet.GetButton(ERSDriftNetButton.OVERLAY_CONFIRM).Click();
