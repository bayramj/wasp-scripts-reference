TPointArray
TPointArray related methods that extend SRL’s TPoint functionality.

TPointArray.ToString
function TPointArray.ToString(): String;
Prints the TPointArray in a way that can be copy pasted into and used by Simba.

Example:

tpa := [[1,1], [2,2], [3,3]];
WriteLn tpa.ToString();
T2DPointArray.Connect
function T2DPointArray.Connect(): T2DPointArray;
Connects each TPointArray in a T2DPointArray. Useful for debugging visually.

Example:

Debug(atpa.Connect());
