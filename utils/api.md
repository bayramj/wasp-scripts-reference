API
Methods related to wasp-api.

type APIClient
type APIClient = record(TSRLBaseRecord) class var
  Disabled: Boolean;
  HTTPClient: Int32;
  StatsServer: String;
  UUID: String;
  Timer: TCountDown;
  TimeStamp: UInt64;
  IsSetup: Boolean;
  Benchmark: TIntegerArray;
  Fails: Int32;
end;
Type responsible for stats submissions. This is basically a simba wrapper for the waspscripts API.

You can find the API docs in https://api.waspscripts.com/docs if you need to read them but the APIClient should be able to do everything for you.

APICLient.SetUsername
procedure TAPICLient.SetUsername(user: String = '');
Sets APICLient username if it hasn’t been set yet.

APIClient.Setup
procedure TAPIClient.Setup();
Internal method automatically called when attempting to use APIClient.GET() and APIClient.POST().

APIClient.GetUUID
function TAPIClient.GetUUID(): String;
Returns your UUID.

Example:

WriteLn APIClient.GetUUID();
APIClient.GetPassword
function TAPIClient.GetPassword(): String;
Returns your Password.

Example:

WriteLn APIClient.GetPassword();
APIClient.GetUsername
function TAPIClient.GetUsername(): String;
Returns your Username.

Example:

WriteLn APIClient.GetUsername();
APIClient.SetLocal
procedure TAPIClient.SetLocal(port: Int32 = 8080);
Method only meant to be used if you are hosting a local stats server for debugging purposes.

APIClient.HashPassword
function TAPIClient.HashPassword(password: String): String;
Returns a salted and hashed password. This serves no purpose other than giving you a glimpse of what is stored in waspscripts database when you submit your password.

Try the example below, notice how everytime you run it you will have slightly different results. That’s the magic of “salting” passwords. You can read more about it on the wikipedia https://en.wikipedia.org/wiki/Salt_(cryptography).

Example:

WriteLn APIClient.HashPassword('helloworld');
WriteLn APIClient.HashPassword(StatsPayload.Password);
APIClient.CheckPassword
function TAPIClient.CheckPassword(password: String): Boolean;
Simply returns true/false if the password you submit matches what is stored in waspscripts stats database for the specified uuid.

Example:

WriteLn APIClient.CheckPassword('0.999999999999999', 'helloworld');
WriteLn APIClient.CheckPassword(APIClient.Generateuuid(), APIClient.GeneratePassword());
APIClient.UpdatePassword
function TAPIClient.UpdatePassword(old, new: String): Boolean;
Because users passwords can be changed and that’s what are used by default for stats password a way to update the stats password is required. That’s what this method is for.

This will probably be complicated for regular users but an easier way can be figured out in the future.

Example:

const
  PASSWORD:     String = 'old_password';
  NEW_PASSWORD: String = 'new_password';
begin
  APIClient.UpdatePassword(PASSWORD, NEW_PASSWORD);
end.
APIClient.CheckStats
function TAPIClient.CheckStats(): String;
Returns your stats.

Example:

WriteLn APIClient.CheckStats();
APIClient.SubmitStats
function TAPIClient.SubmitStats(): Boolean;
Method to submit stats to wasp-stats with the help of StatsPayload.

Example:

StatsPayload.Setup('SCRIPT_ID_HERE', APIClient.GeneratePassword());
StatsPayload.Update(100, 100, 5000);
WriteLn APIClient.SubmitStats(APIClient.Generateuuid());
APIClient.Pause
procedure TAPIClient.Pause();
Method used to pause the APIClient timers.

APIClient.Resume
procedure TAPIClient.Resume();
Method used to resume the APIClient timers.

APIClient.GetScript
APIClient.GetScript(script_id: String; verbose: Boolean = False): String;
Retrieves info of the script with the specified script_id from https://api.waspscripts.com

Example:

APIClient.GetScript('cf0a01e4-8d20-41c2-a78e-3d83081b388d');
APIClient.GetScriptRevision
function TAPIClient.GetScriptRevision(script_id: String; verbose: Boolean = False): Int32;
Retrieves the latest revision number of the script with the specified script_id from https://api.waspscripts.com

Example:

WriteLn APIClient.GetScriptRevision('cf0a01e4-8d20-41c2-a78e-3d83081b388d');
APIClient.GetVersion
function TAPIClient.GetVersion(pkg: String; verbose: Boolean = False): String;
Retrieves the latest version of the package specified from https://api.waspscripts.com.

Example:

WriteLn APIClient.GetVersion('srl-t');
WriteLn APIClient.GetVersion('wasplib');
APIClient.GetAllVersions
function TAPIClient.GetAllVersions(script_id: String; out revision, srltVersion, wlVersion: String; verbose: Boolean = False): String;
Retrieves the latest script revison of script_id and the latest SRL-T and WaspLib versions https://api.waspscripts.com.
