Mouse
Methods to interact with the mouse.

Mouse.Move
procedure TMouse.Move(tpa: TPointArray; forcedMove: Boolean = False); overload;
Moves the mouse to a random point in a TPoint Array.

forcedMove determines if the mouse should be moved if already in a point that is part of the tpa. By default this is False.