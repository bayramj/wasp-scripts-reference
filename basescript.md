BaseScript
BaseScript and it’s derivants are template records to be used in scripts. They also contain template functions and procedures that can be used as is or overriden with “inherited” to add functionality.

type TBaseScript
Record that holds common variables for most basic scripts. The variables that are part of TBaseScript are the following:

Name: String that holds the script name to be displayed in the log and on screen progress report.

Version: String that holds the script version to be displayed in the log and on screen progress report.

Self.IsSetup: Boolean that let us know if the our TBaseScript already set it’s variables up.

TimeRunning: TStopwatch variable that holds how long our TBaseScript has been running.

Action: String variable used to print in Simba output or on screen progress report the current action the script is performing.

PreviousAction: String variable used to register the previous action. This is used to avoid spamming the logs.

ExtraInfo: String variable we can use to print extra information in Simba output or in on screen progress report. E.G. current state of variables.

ActionProfit: Integer that holds information on how much profit (positive or negative) our script makes per action performed.

TotalActions: Integer used to count how many actions our script has done.

TotalProfit: Integer that holds the total profit our script has done.

TimeLimit: Integer variable to set a time limit for our script in milliseconds before ending the current script.

ActionLimit: Integer variable to set total action limit before ending the script.

TBaseScript can be used as is or inherited from to extend it’s functionality.

Example:

TBaseWalkerScript = record(TBaseScript)
  RSW: TRSWalker;
end;
BaseScript.ShouldHandlePaint
function TBaseScript.ShouldHandlePaint(): Boolean;
Wrapper function used internally to decide if we should handle TWaspProgressReport.

BaseScript.ShouldDrawPaint
function TBaseScript.ShouldDrawPaint(): Boolean;
Wrapper function used internally to decide if we should call TWaspProgressReport.Update(). To avoid unnecessary redraw, when Self.Action and Self.PreviousAction are the same, we do not redraw.

BaseScript.BuildTextReport
function TBaseScript.BuildTextReport(): TStringArray;
Internal method used to build our text progress report. To set custom messages simply override this method and pass in each line of you report into the Result array. Keep in mind that editing this will probably mess up the HUD report so if you customize this you should also customize TBaseScript.BuildHUDReport().

Example:

function TBaseScript.BuildTextReport(): TStringArray; override;
var
  ElapsedTime: UInt64;
  XPEarned: Int32;
begin
  ElapsedTime := Self.TimeRunning.ElapsedTime();
  XPEarned := WL.PreviousXP - WL.InitialXP;

  //Keep in mind this is just a quick example without spacing adjustments. This won't look good unless you add some variable padding.

  Result += '[===============================]';
  Result += '[ ' + Self.Name + ' ]';                    //Self.Name is the script name, usually set in TBaseScript.Init();
  Result += '[===============================]';
  Result += '[ Runtime    :  ' + SRL.MsToTime(ElapsedTime, Time_Short) +' ];
  Result += '[ Xp gained  : ' + XPEarned + '(' + ToStr(NumberPerHour(XPEarned, ElapsedTime)) + ' / hr)     ]';
  Result += '[ Nuggets    : ' + NuggetsCount + '(' + ToStr(NumberPerHour(NuggetsCount, ElapsedTime)) + ' / hr)     ]';
  Result += '[ Coal       : ' + CoalCount + '(' + ToStr(NumberPerHour(CoalCount, ElapsedTime)) + ' / hr)     ]';
  Result += '[ Gold       : ' + GoldCount + '(' + ToStr(NumberPerHour(GoldCount, ElapsedTime)) + ' / hr)     ]';
  Result += '[ Mithril    : ' + MithrilCount + '(' + ToStr(NumberPerHour(MithrilCount, ElapsedTime)) + ' / hr)     ]';
  Result += '[ Adamantite : ' + AdamantiteCount + '(' + ToStr(NumberPerHour(AdamantiteCount, ElapsedTime)) + ' / hr)     ]';
  Result += '[ Runite     : ' + RuniteCount + '(' + ToStr(NumberPerHour(RuniteCount, ElapsedTime)) + ' / hr)     ]';
  Result += '[===============================]';
  Result += '[ ' + Self.Name + SRL.MsToTime(ShutdownTimer.TimeRemaining, Time_Short) + ' ]';
  Result += '[===============================]';
end;
BaseScript.PrintReport
procedure TBaseScript.PrintReport(Sender: TObject);
Internal method to print our progress report (“proggie”). This is run on a timer setup by TBaseScript and also handles drawing the HUD progress report if it is enabled. It also is responsible for debugging the script with SRL.Debug() if we enable it.

CheckUpdates
procedure CheckUpdates(caption: String = 'Updates Available');
Checks for updates for SRL-T, WaspLib and the current script.

BaseScript.Init
procedure TBaseScript.Init(maxActions: UInt32; maxTime: UInt64);
Method used to setup the variables of TBaseScript. If maxActions and/or maxTime are not 0 that will make TBaseScript.ShouldStop() = True when TBaseScript.TotalActions = maxAtions or TBaseScript.TimeRunning.ElapsedTime = maxTime.

Can be used as is or overriden to do additional tasks.

Example:

var
  Script: TBaseScript;

begin
  Script.Init(0, 2 * ONE_DAY);
end;
BaseScript.DoAntiban
function TBaseScript.DoAntiban(checkBreaks: Boolean = True; checkSleeps: Boolean = True): Boolean;
Method used to call Antiban.DoAntiban(checkBreaks, checkSleeps).

Example:

Script.DoAntiban();
BaseScript.ShouldStop
function TBaseScript.ShouldStop(): Boolean;
Method used to check if we reached the TBaseScript goals and it’s time to stop it.

Note

This doesn’t stop the script. This simply returns true/false when called and it’s up to you to stop the script.

Example:

if Script.ShouldStop() then
  TerminateScript();
type TBaseWalkerScript
Record that holds common variables for most scripts that use walker. This record extends TBaseScript and has all of it’s variables too. The extra variables that are part of TBaseWalkerScript are:

RSW: TRSWalker variable that holds our walker, for more information check the following page: https://ollydev.github.io/SRL-Development/walker.html?highlight=walker

BaseWalkerScript.Init
procedure TBaseWalkerScript.Init(MaxActions: Int32; MaxTime: Int64); override;
Method used to setup the variables of TBaseScript. If MaxActions and MaxTime serve the same purpose of TBaseScript.Init().

Can be used as is or overriden to do additional tasks.

type TBaseBankScript
Record that holds common variables for most scripts that use a bank. This record inherits from TBaseWalkerScript and which inherits from TBaseScript’s. The extra variables that are part of TBaseBankScript are:

Self.ScriptBank: PRSObject pointer that points to our current bank TRSObject, for more info check: https://torwent.github.io/WaspLib/waspobject.html#type-trsobject

Self.ScriptBanker: PRSNPC pointer that points to our current banker TRSNPC, for more info check: https://torwent.github.io/WaspLib/waspobject.html#type-trsmmdot

BankTab: Integer variable used to cache the current bank tab that contains items for our script.

ItemLeftAmount: Integer variable used to cache items left to make/build/whatever to pre-hover the bank.

HoveringBank: Boolean variable that holds information if we are currently already hovering the bank. This is so we don’t try to rehover the bank and don’t need to check the uptext if we already are doing it.

BankEmpty: Boolean variable that that is set to true when we ran out of an item our script needs. This is used so next time we need to fetch the item we check the deposit box instead.

CollectEmpty: Boolean variable that that is set to true when the collect box is empty. Normally, if this and BankEmpty are true the script ends.

CollectTimer: TCountDown variable used to reset CollectEmpty after a couple of minutes.

BaseBankScript.Init
procedure TBaseBankScript.Init(MaxActions: UInt32; MaxTime: UInt64); override;
Method used to setup the variables of TBaseScript. If MaxActions and MaxTime serve the same purpose of TBaseScript.Init().

Can be used as is or overriden to do additional tasks.

BaseBankScript.Terminate
function TBaseBankScript.Terminate(): Boolean;
Helper method to be called at the end of the life cycle of a TBaseBankScript. By default it simply attempts to open the TBaseBankScript.CurrentBank but it’s meant to be overriden and inherited or completely be remade for proper termination of the TBaseBankScript.

This is likely required if you want to chain several scripts together.

Note

Consider taking a look at script_chainer.simba: https://github.com/Torwent/wasp-mini/blob/master/script_chainer.simba

Example:

Script1.Init();
repeat
  //do stuff...
until Script1.ShouldStop();

Script1.Terminate();

Script2.Init();
repeat
  //do stuff...
until Script2.ShouldStop();
BaseBankScript.CountItemsLeft
procedure TBaseBankScript.CountItemsLeft(Item: TRSItem);
Set’s TBaseBankScript.ItemLeftAmount to be used by TBaseBankScript.ShouldHover().

Note

For some scripts this might need to be overriten and rewritten.

BaseBankScript.ShouldHoverBank
function TBaseBankScript.ShouldHoverBank(): Boolean;
Method used to decide if we should pre-hover the bank or not. It uses the amount of items left in the inventory stored by TBaseBankScript.CountItemsLeft() in TBaseBankScript.ItemLeftAmount() along with the player BioHash to decide if we want to pre-hover the bank.

Note

This function simply returns true/false and doesn’t actualy hover the bank.

Example:

if Script.ShouldHoverBank() then
  Script.HoverBank();
BaseBankScript.HoverBank
function TBaseBankScript.HoverBank(): Boolean;
Moves the mouse to the closest RSObjects.Banks

Example:

BankScript.HoverBank();
BaseBankScript.Withdraw
function TBaseBankScript.Withdraw(item: TRSBankWithdrawItem): Boolean;
Withdraws item from the bank.

Example:

item := TRSBankItem.Setup('Shark', 1, True);
if Bank.IsOpen() then
  BankScript.Withdraw(item);
BaseBankScript.DepositItem
function TBaseBankScript.DepositItem(out item: TRSBankItem; isBank, isDepositBox: Boolean = False): Boolean;
function TBaseBankScript.DepositItem(item: TRSItem; isBank, isDepositBox: Boolean = False): Boolean; overload;
Deposits item in the bank through either the bank or deposit box depending on which one is open.

BaseBankScript.DepositItems
function TBaseBankScript.DepositItem(out items: TRSBankItemArray; isBank, isDepositBox: Boolean = False): Boolean;
function TBaseBankScript.DepositItems(item: TRSItem; isBank, isDepositBox: Boolean = False): Boolean; overload;
Deposits item in the bank through either the bank or deposit box depending on which one is open.

BaseBankScript.HandleCollectBox
function TBaseBankScript.HandleCollectBox(items: TRSItemArray): Boolean;
Collects items from the collectbox.

Example:

if CollectBox.IsOpen() then
  BankScript.HandleCollectBox();