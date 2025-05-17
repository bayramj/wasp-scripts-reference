Math
This file has math related methods.

Double.GetDigit
function Double.GetDigit(n: Int32): Integer;
Get the digit at the nth place of the Double.

Credits: Slacky

Example:

var
  BioHash := 0.0123456789;
begin
  WriteLn BioHash.GetDigit(4); //will print 3
end;
NumberPerHour
function NumberPerHour(n: Int64): Int32;
function NumberPerHour(n: Double): Int32; overload;
Calculate how many n per hour. You can optionally specify the amount of time to use in the calculation.

Example:

WriteLn NumberPerHour(10000, 2 * ONE_HOUR); //will print 5000.