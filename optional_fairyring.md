FairyRing
Fairy rings interface.

FairyRing.Setup
procedure FairyRing.Setup();
Initializes TRSFairyRing variables.

Note

This is automatically called on the FairyRing variable.

FairyRing.IsOpen
function TRSFairyRing.IsOpen(): Boolean;
Returns true/false whether the FairyRing interface is open or not.

Example:

 WriteLn FairyRing.IsOpen();
FairyRing.Close
function TRSFairyRing.Close(pressEscape: Boolean): Boolean;
function TRSFairyRing.Close(chance: Double = BioHash): Boolean; overload;
Closes the FairyRing interface, depending on pressEscape the function will either click the button or press escape.

Example:

 WriteLn FairyRing.Close();
FairyRing.HandleItem
function TRSFairyRing.HandleItem(): Boolean;
Magically finds, caches for next usages and equips dramen or lunar staff with the minimum tab opening possible. If no item is found, we will assume the user has the elite lumbridge and draynor diary complete for next uses.

Example:

 if FairyRing.HandleItem() then
WriteLn FairyRing.Item;
FairyRing.Open
function TRSFairyRing.Open(): Boolean;
Attempts to open the closest fairy ring RSObject.

Example:

 WriteLn FairyRing.Open();
FairyRing.WalkOpen
function TRSFairyRing.WalkOpen(): Boolean;
Attempts to walk to if needed and open the closest fairy ring RSObject.

Example:

 WriteLn FairyRing.WalkOpen();
FairyRing.IsLetterValid
function TRSFairyRing.IsLetterValid(letter: Char; dial: ERSFairyRingDial): Boolean;
Checks if the letter passed on is valid for the given dial.

Example:

 WriteLn FairyRing.IsLetterValid('z', ERSFairyRingDial.LEFT);
FairyRing.IsCodeValid
function TRSFairyRing.IsCodeValid(code: String): Boolean;
Checks if the a given code is a valid fairy ring code.

Example:

 WriteLn FairyRing.IsCodeValid('abc');
FairyRing.GetLetterBox
function TRSFairyRing.GetLetterBox(dial: ERSFairyRingDial): TBox;
Returns the current letter box of a fairy ring dial.

Example:

 Debug(FairyRing.GetLetterBox(ERSFairyRingDial.MIDDLE));
FairyRing.GetLetter
function TRSFairyRing.GetLetter(dial: ERSFairyRingDial): Char;
Returns the letter of a fairy ring dial.

Example:

 WriteLn FairyRing.GetLetter(ERSFairyRingDial.RIGHT);
FairyRing.GetCurrentCode
function TRSFairyRing.GetCurrentCode(): String;
Returns the full current fairy ring code set in the dials.

Example:

 WriteLn FairyRing.GetCurrentCode();
FairyRing.GetRotationBox
function TRSFairyRing.GetLeftRotationBox(dial: ERSFairyRingDial): TBox;
function TRSFairyRing.GetRightRotationBox(dial: ERSFairyRingDial): TBox;
Returns the left or right rotation box of the given dial.

Example:

 Debug(FairyRing.GetLeftRotationBox(ERSFairyRingDial.LEFT));
FairyRing.Spin
function TRSFairyRing.SpinLeft(dial: ERSFairyRingDial; skipWait: Boolean = False): Boolean;
function TRSFairyRing.SpinRight(dial: ERSFairyRingDial; skipWait: Boolean = False): Boolean;
Spins the given dial left or right. By default it waits for the rotation to finish but it can be skipped with skipWait.

Example:

 WriteLn FairyRing.SpinLeft(ERSFairyRingDial.LEFT);
FairyRing.SetDial
function TRSFairyRing.SetDial(letter: Char; dial: ERSFairyRingDial; skipWait: Boolean = False): Boolean;
Spins the dial so that the current selected letter is the specified one.

Example:

 WriteLn FairyRing.SetDial('c', ERSFairyRingDial.LEFT);
FairyRing.DialCode
function TRSFairyRing.DialCode(code: String; attempts: Int32 = 3): Boolean;
Dials in a full code on the fairy ring. Codes casing is ignored. attempts is a helper parameter and shouldn’t be touched if you don’t know what you are doing.

Example:

 WriteLn FairyRing.DialCode('cip');
FairyRing.GetTeleportButton
function TRSFairyRing.GetTeleportButton(): TBox;
Returns the box of the teleport button.

Example:

 Debug(FairyRing.GetTeleportButton());
FairyRing.ClickTeleportButton
function TRSFairyRing.ClickTeleportButton(): Boolean;
Clicks the fairy ring the teleport button.

Example:

 WriteLn FairyRing.ClickTeleportButton();
FairyRing.GetLogCodes
function TRSFairyRing.GetLogCodes(out boxes: TBoxArray): TStringArray;
function TRSFairyRing.GetLogCodes(): TStringArray; overload;
Returns the visible codes in the fairy ring travel log.

Example:

 WriteLn FairyRing.GetLogCodes();
FairyRing.FindLogCode
function TRSFairyRing.FindLogCode(code: String; out b: TBox): Boolean;
function TRSFairyRing.FindLogCode(code: String): Boolean; overload;
Finds the code specified in the travel log. Codes casing is ignored.

Example:

 WriteLn FairyRing.FindLogCode('cip');
FairyRing.ClickLogCode
function TRSFairyRing.ClickLogCode(code: String): Boolean;
Finds and clicks the code specified in the travel log. Codes casing is ignored.

Example:

 WriteLn FairyRing.ClickLogCode('cip');
FairyRing.HandleInterface
function TRSFairyRing.HandleInterface(code: String): Boolean;
Completely handles the fairy ring interface to set a code and teleport. Will use both the log and the dials depending on the user biohash.

Example:

 WriteLn FairyRing.HandleInterface('cip');
FairyRing.Teleport
function TRSFairyRing.Teleport(code: String): Boolean;
Teleports the user to the specified fairy ring code. If the fairy ring interface is not open, the RSObject will be used to find the closest one and open it. If the code is on the right click context menu, it will be used. You can also optional pass in “Zanaris” or “BKS” to go to zanaris.

Example:

 WriteLn FairyRing.Teleport('cip');
FairyRing.WalkTeleport
function TRSFairyRing.WalkTeleport(code: String): Boolean;
Teleports the user to the specified fairy ring code. If the fairy ring interface is not open, the RSObject will be used to find the closest one and open it. If the fairy ring is not visible, we will walk to it. If the code is on the right click context menu, it will be used. You can also optional pass in “Zanaris” or “BKS” to go to zanaris.

Example:

 WriteLn FairyRing.Teleport('cip');
var FairyRing
Global FairyRing variable.