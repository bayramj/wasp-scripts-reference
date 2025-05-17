Config
A full featured JSON config writer and reader.

type TConfigJSON
TConfigJSON = record
  Path: String;
  JSON: TJSONObject;
end;
TConfigJSON.GetConfig
function TConfigJSON.GetConfig(): TJSONObject;
Helper method to return the current TConfigJSON.Path file as a TJSONObject. You probably don’t need to use this directly.

TConfigJSON.Free
procedure TConfigJSON.Free();
Used to free your TConfigJSON. It’s automatically called on script termination, but you may call it sooner if you wish to unlock the ram used by this (which should be minimal).

TConfigJSON.Setup
procedure TConfigJSON.Setup(jsonFile: String);
Main method to setup your TConfigJSON

TConfigJSON.DeleteConfig
procedure TConfigJSON.DeleteConfig();
Delete your TConfigJSON from disk.

TConfigJSON.SaveConfig
procedure TConfigJSON.SaveConfig();
Used to save your TConfigJSON. By default, this is always called automatically whenever the config is modified by the TConfigJSON.Put() methods.

TConfigJSON.Put
procedure TConfigJSON.Put(key, value: String; save: Boolean = True);
procedure TConfigJSON.Put(key: String; value: Int32; save: Boolean = True); overload;
procedure TConfigJSON.Put(key: String; value: Double; save: Boolean = True); overload;
procedure TConfigJSON.Put(key: String; value: Boolean; save: Boolean = True); overload;
procedure TConfigJSON.Put(key: String; value: Pointer; save: Boolean = True); overload;
This should be self explanatory. Put a key and a value pair into your TConfigJSON. The pointer version of the method is the only one that might need a little bit more knowledge of Simba’s lower JSON methods and/or pointers but you can use it to place a value that is another JSON object or a JSON array.

TConfigJSON.Has
function TConfigJSON.Has(key: String; nullIsValid: Boolean = True): Boolean;
Checks if a key exists. nullIsValid is true by default when set to false this will return false if the key exists but is set to null.

TConfigJSON.Get
function TConfigJSON.GetString(key: String): String;
function TConfigJSON.GetInt(key: String): Int32;
function TConfigJSON.GetDouble(key: String): Double;
function TConfigJSON.GetBoolean(key: String): Boolean;
function TConfigJSON.GetNull(key: String): Boolean;
function TConfigJSON.GetObject(key: String): TJSONObject;
function TConfigJSON.GetArray(key: String): TJSONArray;
This should be self explanatory. Returns the value of a key in your TConfigJSON. The Object version of the method is the only one that might need a little bit more knowledge of Simba’s lower JSON methods and/or pointers but you can use it to return a JSON object or a TJSONArray of TJSONObjects.

TConfigJSON.Remove
procedure TConfigJSON.Remove(key: String);
Remove a key and it’s respective value from your TConfigJSON.

TConfigJSON.ToString
function TConfigJSON.ToString(indentFactor: Int32 = 2): String;
Returns a string version of your TConfigJSON.

Example:

WriteLn MyConfig.ToString();
type TConfigINI
TConfigINI = record
  Path: String;
  FileName: String;
end;
Example:

ConfigINI.Setup('MyScriptSettings.ini'); // Set file path
ConfigINI.Put('GUISettings', 'UsePoolPOH', 'True'); // Write setting
WriteLn(ConfigINI.Get('GUISettings', 'UsePoolPOH')); // Read setting
WriteLn(ConfigINI.GetKeys('GUISettings')); // List all keys in 'GUISettings'
TConfigINI.Setup
procedure TConfigINI.Setup(ConfigName: String);
Initializes configuration path and filename.

Example:

ConfigINI.Setup('MyScriptSettings.ini');
TConfigINI.Put
procedure TConfigINI.Put(Section, KeyName, Value: String);
Writes a single key-value pair to a specified section.

Example:

ConfigINI.Put('GUISettings', 'UsePoolPOH', 'True');
TConfigINI.Get
function TConfigINI.Get(Section, KeyName: String): String;
function TConfigINI.Get(Section, KeyName, DefaultValue: String): String; overload;
Retrieves a single value by key from a specified section.

Example:

WriteLn(ConfigINI.Get('GUISettings', 'UsePoolPOH'));
TConfigINI.GetKeys
function TConfigINI.GetKeys(Section: String): TStringArray;
Retrieves all keys from a specified section.

Example:

WriteLn(ConfigINI.GetKeys('GUISettings'));
TConfigINI.Remove
procedure TConfigINI.Remove(Section, KeyName: String);
Removes a single key-value pair from a specified section.

Example:

ConfigINI.Remove('GUISettings', 'UsePoolPOH'));
TConfigINI.DeleteConfig
procedure TConfigINI.DeleteConfig();
Deletes the entire configuration file.

Example:

ConfigINI.DeleteConfig();