CollectBox
Methods to interact with the CollectBox.

CollectBox.Setup
procedure CollectBox.Setup();
Initializes CollectBox variables.

Note

This is automatically called on the CollectBox variable.

CollectBox.Close
function TRSCollectBox.Close(UseKeyboard: Boolean = False): Boolean;
Closes the CollectBox, Depending on UseKeyboard the function will either click the button or press backspace.

Example:

 WriteLn CollectBox.Close;
var CollectBox
Global CollectBox variable.