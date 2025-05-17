Color
Color tools.

type SRLColors
Type that holds a large amount of color wrappers so you don’t have to memorize then.

Some colors are duplicated. They are kept for easy name access.

Example:

WriteLn SRLColors.BLACK;
WriteLn SRLColors.ORANGE;
WriteLn SRLColors.BLUE;
GetNextCycleColor
function GetNextCycleColor(color, step: Int32): Int32;
Not currently used for anything, just a fun experiment. Can be used to give an RGB cycle effect.

RGB2BGR
function RGB2BGR(rgb: Int32): Int32;
function RGB2BGR(rgb: String): Int32; overload;
Converts an RGB color to BGR.

Note

credits go to slacky.

Example:

WriteLn RGB2BGR($00FFAA);
