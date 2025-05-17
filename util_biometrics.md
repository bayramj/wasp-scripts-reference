Biometrics
Methods related to biometrics that make your account behave in a unique way.

GenerateUUIDV4
function GenerateUUIDV4(): String;
Generate a UUID.

Example:

WriteLn GenerateUUIDV4();
var BioHash
Global BioHash variable. BioHash is a unique ID of each account and can be used to influence several things.

var BioHashOverride
Global BioHashOverride variable. If set, will override whatever would be generated for BioHash instead.

type EBioBehavior
EBioBehavior = (
  MOUSE_SPEED,
  MOUSE_GRAVITY,
  MOUSE_WIND,
  MOUSE_MISS,
  FKEY_CHANCE,
  ESCAPE_CHANCE,
  KEYBOARD_CHAT_CHANCE,
  REACTION_SPEED,
  SPAM_CLICK_CHANCE,
  DROP_PATTERN,
  CONSUME_IN_BANK,
  USES_LIKE_BUTTONS,
  TENDS_TO_LIKE
);
EBioBehavior is a enum that represent biohaviors affected by the user BioHash.

Antiban.SetupBiometrics
procedure TAntiban.SetupBiometrics();
This comes straight from older SRL versions. This basically sets up our BioHash which is a hash of the current player login username. Because usernames are unique, so will the BioHash.

Antiban.GetBehavior
function TAntiban.GetBehavior(behavior: EBioBehavior): Int32;
Get the value that corresponds to the specified behavior.

Example:

WriteLn Antiban.GetBehavior(FKEY_CHANCE);
Antiban.GetChance
function TAntiban.GetChance(behavior: EBioBehavior): Double;
Get a probability from the current biohash that is represented by behavior.

Example:

WriteLn Antiban.GetChance(FKEY_CHANCE);
Antiban.GetMultiplier
function TAntiban.GetMultiplier(): Double;
This generates a random seed number that is influenced by BioHash. There are times you will not want to use BioHash itself because it’s value is static, this function let’s you get a seed number that is random but heavily influenced by BioHash. Values returned by this range between 0 and 2. So if you are multiplying something by this, your result will be between 0 and 200%.

Example:

Wait(Round(3000 * Antiban.GetMultiplier())));
Antiban.GetUniqueNumber
function TAntiban.GetUniqueDouble(input: Double): Double;
function TAntiban.GetUniqueDouble(input, min, max: Double): Double; overload;
function TAntiban.GetUniqueDouble(input, min: Double): Double; overload;
function TAntiban.GetUniqueInt(input: Int64): Int64;
function TAntiban.GetUniqueInt(input, min, max: Int64): Int64; overload;
function TAntiban.GetUniqueInt(input, min: Int64): Int64; overload;
These generate a unique number based on your input and you BioHash. The overloaded methods allow you to use some extra parameters for this to cap the results at a min and max value.

Example:

FoodAmount := Antiban.GetUniqueInt(7, 3, 15);
Antiban.GetUniqueAverage
function TAntiban.GetUniqueDoubleAverage(input: Double; Iterations: Integer): Double;
function TAntiban.GetUniqueDoubleAverage(input, Sum: Double; Iterations: Integer): Double; overload;
function TAntiban.GetUniqueDoubleAverage(input, min, max: Double; Iterations: Integer): Double; overload;
function TAntiban.GetUniqueIntAverage(input: Int64; iterations: Int32): Int64;
function TAntiban.GetUniqueIntAverage(input, min: Int64; iterations: Int32): Int64; overload;
function TAntiban.GetUniqueIntAverage(input, min, max: Int64; iterations: Int32): Int64; overload;
Functions to test Antiban.GetUniqueNumber.

THIS IS ONLY MEANT FOR DEBUGGING!

It will run Antiban.GetUniqueNumber for how many Iterations you specify and average the results out. Useful to know more or less what result to expect from your input.

Example:

WriteLn Antiban.GetUniqueAverage(7, 3, 15, 500);
Antiban.BioDice
function TAntiban.BioDice(): Boolean;
function TAntiban.BioDice(behaviour: EBioBehavior): Boolean; overload;
function TAntiban.BioDice(chance: Double): Boolean; overload;
Throws a SRL.Dice heavily skewed in certain directions depending on your BioHash and the parameters passed in.

Example:

UseBankEarly := Antiban.BioDice();
WriteLn UseBankEarly;
Antiban.GetSleepHour
function TAntiban.GetSleepHour(): String;
Sets WLSettings.Sleep.Hour based on the current BioHash. WLSettings.Sleep.HourOverride will override this.

Example:

Antiban.SetSleepHour();
WriteLn WLSettings.Sleep.Hour;
Antiban.GetSleepLength
function TAntiban.GetSleepLength(): Single;
Gets WLSettings.Sleep.Length based on the current BioHash. WLSettings.Sleep.LengthOverride will override this.

Example:

Antiban.SetSleepLength();
WriteLn WLSettings.Sleep.Length;
Antiban.Wait
procedure TAntiban.BioWait(time: UInt32);
procedure TAntiban.BioWait(min, max: UInt32; weight: EWaitDir = wdMean); overload;
Wait() but skewed with BioHash.

Example:

Inventory.Open()
Antiban.Wait(4000);
Magic.Open();
Antiban.Click
procedure TAntiban.Click(button: Int32; min: Int32 = 1, max: Int32 = 3);
Mouse.Click() with a BioHashed probability of spam clicking between 0.

Example:

Inventory.HoverSlot(5);
Antiban.Click(MOUSE_LEFT);