String.Case
function String.CamelCase(): String; constref;
function String.SnakeCase(): String; constref;
function String.UpperSnakeCase(): String; constref;
function String.KebabCase(): String; constref;
function String.PascalCase(): String; constref;
function String.SentenceCase(): String; constref;
function String.TitleCase(): String; constref;
Returns the string with different forms of capitalization.

Example

var
  str: String = 'HELLO WORLD';
begin
  WriteLn str.TitleCase(); //Prints 'Hello World'
end;
