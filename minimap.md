Minimap
Methods to handle Minimap. Extends SRL’s Minimap.

Minimap.WaitMoving
procedure TRSMinimap.WaitMoving(doAntiban: Boolean = True);
Gives Minimap.WaitPlayerMoving the ability to perform antiban tasks while moving.

Example:

Minimap.WaitMoving();
Minimap.OnGroundLevel
function TRSMinimap.OnGroundLevel(threshold: Int32 = 3300): Boolean;
Minimap.OnGroundLevel returns true if we are likely to be on the ground level. This works by counting the amount of black in the minimap and might give false positives/negatives if there’s more than 3500 black pixels on the minimap. A threshold can be set for this counting, the default being 3300.

Example:

WriteLn Minimap.OnGroundLevel();
Minimap.InPOH
function TRSMinimap.InPOH();
Minimap.InPOH returns true if we are in a POH. This might give false positives if you are upstairs or in a place with few colors on the minimap. It might also give false negatives if the POH is crowded.

Example:

WriteLn Minimap.InPOH();
Minimap.FindArrow
function TRSMinimap.FindRedArrow(out tpa: TPointArray): Boolean;
function TRSMinimap.FindRedArrow(): Boolean; overload;
function TRSMinimap.FindYellowArrow(out tpa: TPointArray): Boolean;
function TRSMinimap.FindYellowArrow(): Boolean; overload;
function TRSMinimap.FindArrow(out tpa: TPointArray): Boolean;
function TRSMinimap.FindArrow(): Boolean; overload;
Returns true if there’s a an arrow on minimap. If a TPointArray is passed as a parameter it will return with the location of the arrow.

Example:

Writeln Minimap.FindArrow();
Minimap.WaitArrow
function TRSMinimap.WaitRedArrow(tpa: TPointArray; waitTime: Int32 = 600; interval: Int32 = -1): Boolean;
function TRSMinimap.WaitRedArrow(waitTime: Int32 = 600; interval: Int32 = -1): Boolean;
function TRSMinimap.WaitYellowArrow(tpa: TPointArray; waitTime: Int32 = 600; interval: Int32 = -1): Boolean;
function TRSMinimap.WaitYellowArrow(waitTime: Int32 = 600; interval: Int32 = -1): Boolean;
function TRSMinimap.WaitArrow(tpa: TPointArray; waitTime: Int32 = 600; interval: Int32 = -1): Boolean;
function TRSMinimap.WaitArrow(waitTime: Int32 = 600; interval: Int32 = -1): Boolean;
Waits waitTime for a an arrow to appear on Minimap. If a TPointArray is passed as a parameter it will return with the location of the arrow tip.

Example:

Writeln Minimap.WaitArrow();
Minimap.HasDotUnder
function TRSMinimap.HasDotUnder(): Boolean;
Checks if the player has a dot under it. This will include all types of ERSMinimapDot.

Example:

Writeln Minimap.HasDotUnder();