RSCacheParser
RSCacheParser as the name implies is a record made to parse information from certain files that are part of the OSRS cache.

preferences.dat is where most client settings are stored.

preferences2.dat I have no idea? some values in address 00000020 seem to change after some times has passed randomly. (related to 6h log maybe!?!?)

random.dat in the user home directory seems to be a random identifier generated the first time you open a client if it doesn’t exist. while it exists, it seems to never change unless the user deletes it.

Note

For more information check this file: https://github.com/open-osrs/runelite/blob/dd4478eff7d90fcb3e85584171d5836809eb150a/runescape-client/src/main/java/ClientPreferences.java

type TRSCacheParser
type
  TRSCacheParser = record(TSRLBaseRecord)
    Disabled: Boolean;
    Directory: String;
    Preferences: String;
    Preferences2: String;
  end;
Type responsible for handling osrs cache parsing.

RSCacheParser.Setup
procedure TRSCacheParser.Setup();
Internal method called automatically simply by including WaspLib.

RSCacheParser.GetPreference
function TRSCacheParser.GetPreference(prefNumber: Int32 = 1): String;
Read the preference file specified.

RSCacheParser.Update
function TRSCacheParser.Update(): Boolean;
Method to check if the cache files were updated.

RSCacheParser.GetHexString
function TRSCacheParser.GetHexString(prefNumber: Int32 = 1): String;
Print the cache files as a hex string.

Example:

WriteLn RSCacheParser.GetHexString(1);
RSCacheParser.Print
procedure TRSCacheParser.Print(prefNumber: Int32 = 0);
Print the cache files as strings. This is only useful for debugging purposes.

Example:

RSCacheParser.Print();
RSCacheParser.GetOptionsAmount
function TRSCacheParser.GetOptionsAmount(): Int32;
Returns the number of options saved in the cache. This is not very useful, AFAIK there’s only 2 possible values for this: 0 and 10. 0 is only if you haven’t accepted the EULA in the client.

Example:

WriteLn RSCacheParser.GetOptionsAmount();
RSCacheParser.RoofsHidden
function TRSCacheParser.RoofsHidden(): Boolean;
Checks if the roofs are hidden.

Example:

WriteLn RSCacheParser.RoofsHidden();
RSCacheParser.TitleMusicDisabled
function TRSCacheParser.TitleMusicDisabled(): Boolean;
Checks if the music is enabled in the login screen.

Example:

WriteLn RSCacheParser.TitleMusicDisabled();
RSCacheParser.WindowMode
function TRSCacheParser.WindowMode(): Int32;
Returns 1 for fixed mode and 2 for resizable mode. Resizable modern and resizable classic make no difference here.

Example:

WriteLn RSCacheParser.WindowMode();
RSCacheParser.GetAuthenticatorAmount
function TRSCacheParser.GetAuthenticatorAmount(): Int32;
Returns the number of authenticators saved for the next 30 days. If this is more than 0, you will have 8 bytes for each of the saved authenticators. This is important to know so we know where the saved username starts if we have saved authenticators.

Example:

WriteLn RSCacheParser.GetAuthenticatorAmount();
RSCacheParser.GetAuthenticators
function TRSCacheParser.GetAuthenticators(): TStringArray;
Returns each authenticator saved in a TStringArray. Each string is 8 bytes like mentioned in RSCacheParser.GetAuthenticatorAmount() documentation.

Example:

WriteLn RSCacheParser.GetAuthenticators();
RSCacheParser.GetUsernameIndex
function TRSCacheParser.GetUsernameIndex(): Int32;
Internal function that returns byte index where the username starts. This is required because depending on wether we have authenticators saved or not, the bytes shift.

RSCacheParser.GetUsername
function TRSCacheParser.GetUsername(): String;
Returns the saved username in the osrs cache. This is the username you clicked to save on the client when logging in.

Example:

WriteLn RSCacheParser.GetUsername();
RSCacheParser.UsernameEndIndex
function TRSCacheParser.UsernameEndIndex(): Int32;
Internal function used to get the index of the byte of where the username ends.

RSCacheParser.HideUsername
function TRSCacheParser.HideUsername(): Boolean;
Returns true or false if we have the username hidden.

Example:

WriteLn RSCacheParser.HideUsername();
RSCacheParser.Brightness
function TRSCacheParser.Brightness(): Int32;
Returns the brightness value converted to a 0-100 value.

Example:

WriteLn RSCacheParser.Brightness();
RSCacheParser.MusicVolume
function TRSCacheParser.MusicVolume(): Int32;
Returns the music volume value converted to a 0-100 value.

Example:

WriteLn RSCacheParser.MusicVolume();
RSCacheParser.SoundEffectsVolume
function TRSCacheParser.SoundEffectsVolume(): Int32;
Returns the sound effects volume value converted to a 0-100 value.

Example:

WriteLn RSCacheParser.SoundEffectsVolume();
RSCacheParser.AreaSoundVolume
function TRSCacheParser.AreaSoundVolume(): Int32;
Returns the area sound volume value converted to a 0-100 value.

Example:

WriteLn RSCacheParser.AreaSoundVolume();
RSCacheParser.Field1247
function TRSCacheParser.Field1247(): Int32;
I have absolutely no idea what this is. It’s supposedly something, but AFAIK it’s always 0.

Example:

WriteLn RSCacheParser.Field1247();
RSCacheParser.DisplayFPS
function TRSCacheParser.DisplayFPS(): Boolean;
Returns true/false if we have Display FPS enabled. Display FPS can be enabled by typing ::displayfps in game.

Example:

WriteLn RSCacheParser.DisplayFPS();
RSCacheParser.Field1238
function TRSCacheParser.Field1238(): Int32;
I have absolutely no idea what this is. It’s supposedly something, but AFAIK it’s always 0.

Example:

WriteLn RSCacheParser.Field1238();
