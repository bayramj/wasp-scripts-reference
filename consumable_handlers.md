ConsumableHandlers
ConsumableHandlers are responsible for handle all kinds of consumables in WaspLib. For a list of the consumable types check ERSConsumable, there’s a TConsumableHandler for each one.

type TConsumableHandler
  TConsumableHandler = record(TSRLBaseRecord)
    ConsumableType: ERSConsumable;
    ConsumableArray: TRSConsumableArray;
    Amount, MinInvPoints: Int32;
    Timer, Delay: TCountDown;
    IsSetup: Boolean;
  end;
Consumable handler is the record responsible to handle TRSConsumables <https://torwent.github.io/WaspLib/consumables.html>_. This will handle caching all found consumables to this point, bank withdraw amounts, timer if the last consumable had a timer, etc.

type PConsumableHandler
PConsumableHandler = ^TConsumableHandler;
Wrapper type of a TConsumableHandler pointer.

ConsumableHandler.Setup()
function TConsumableHandler.Setup(Item: TRSItem): TRSConsumable;
procedure TConsumableHandler.Setup(consumableType: ERSConsumable); overload;
Used internally to add a TRSConumable to TConsumableHandler.ConsumableArray.

The overloaded method is used to setup TConsumableHandler.ConsumableArray with a TConsumableHandler.ConsumableType. This will use TConsumableHandler.FindInInventory() or TConsumableHandler.FindInBank() by that order to setup found TRSConsumables.

Example:

FoodHandler.Setup('Shark');
FoodHandler.Setup(ERSConsumable.FOOD);
ConsumableHandler.FindInBank()
function TConsumableHandler.FindInBank(): TRSConsumableArray;
Returns an TRSConsumableArray of all TRSConsumables of TConsumableHandler.consumableType found in the bank window.

ConsumableHandler.FindInInventory()
function TConsumableHandler.FindInInventory(): TRSConsumableArray;
Returns an TRSConsumableArray of all TRSConsumables of TConsumableHandler.ConsumableType found in the inventory.

ConsumableHandler.NeedToConsume()
function TConsumableHandler.NeedToConsume(): Boolean;
Returns an True if there’s a timer setup and it has ran out.

var Handlers
FoodHandler:          TConsumableHandler;
PrayerHandler:        TConsumableHandler;
EnergyHandler:        TConsumableHandler;
PoisonHandler:        TConsumableHandler;
AntifireHandler:      TConsumableHandler;
BoostHandler:         TConsumableHandler;
StrengthBoostHandler: TConsumableHandler;
AttackBoostHandler:   TConsumableHandler;
DefenceBoostHandler:  TConsumableHandler;
RangingBoostHandler:  TConsumableHandler;
MagicBoostHandler:    TConsumableHandler;

CONSUMABLE_HANDLER_ARRAY: array [ERSConsumable] of PConsumableHandler := [
  @FoodHandler, @PrayerHandler, @EnergyHandler, @PoisonHandler,
  @AntifireHandler, @BoostHandler, @StrengthBoostHandler, @AttackBoostHandler,
  @DefenceBoostHandler, @RangingBoostHandler, @MagicBoostHandler
];
Global handler variables. This handlers are the ones responsible for handling consumables.

ConsumableHandler.GetHandler()
function TConsumableHandler.GetHandler(consumableType: ERSConsumable): PConsumableHandler; static;
Static method to return a pointer to the right handler for each consumableType passed in.

Inventory.FindItems()
function TRSInventory.FindItems(Items: TRSConsumableArray; out FoundItems: TRSConsumableArray; out Slots: TIntegerArray): Boolean; overload;
Method used to find consumables in the inventory. Can be used directly but in most cases is used internally.

Inventory.FindConsumable()
function TRSInventory.FindConsumable(consumableType: ERSConsumable; out FoundConsumables: TRSConsumableArray; out Slots: TIntegerArray): Boolean;
function TRSInventory.FindConsumable(consumableType: ERSConsumable): Boolean; overload;
Method used to find already setup consumables in the inventory. Can be used directly but in most cases is used internally.

Inventory.Consume
function TRSInventory.Consume(consumableType: ERSConsumable; out Slots: TIntegerArray): Boolean;
function TRSInventory.Consume(consumableType: ERSConsumable): Boolean; overload;
Methods used to consume consumables.

Example:

Inventory.Consume(ERSConsumable.FOOD);
Inventory.CountConsumable()
function TRSInventory.CountConsumable(consumableType: ERSConsumable): Int32;
Method used to count each slot that has a consumable of consumableType.

Example:

WriteLn Inventory.CountConsumable(ERSConsumable.FOOD);
Inventory.CountEachConsumable()
function TRSInventory.CountEachConsumable(consumableType: ERSConsumable): TIntegerArray;
Method used to count each type of consumable of consumableType.

Example:

WriteLn Inventory.CountEachConsumable(ERSConsumable.FOOD);
Inventory.CountPoints()
function TRSInventory.CountPoints(Consumable: TRSConsumable): Int32;
function TRSInventory.CountPoints(consumableType: ERSConsumable): Int32; overload;
Method used to count the total points value of a Consumable or consumableType.

Example:

WriteLn Inventory.CountPoints(ERSConsumable.FOOD); //Assumind you have 3 sharks in your inventory, 60 will be printed.
Inventory.HasEnoughConsumable()
function TRSInventory.HasEnoughConsumable(consumableType: ERSConsumable): Boolean;
Method used to figure out if we are low on a type of consumable.

Example:

if not Inventory.HasEnoughConsumable(ERSConsumable.FOOD) then
  Bank.WithdrawItem(['Shark', 5, False], False);
Bank.FindConsumable()
function TRSBank.FindConsumable(ConsumableArray: TRSConsumableArray; out Consumable: TRSConsumable): Boolean;
function TRSBank.FindConsumable(ConsumableArray: TRSConsumableArray): Boolean; overload;
function TRSBank.FindConsumable(consumableType: ERSConsumable; out Consumable: TRSConsumable): Boolean; overload;
function TRSBank.FindConsumable(consumableType: ERSConsumable): Boolean; overload;
Method used to find already setup consumables in the bank. Can be used directly but in most cases is used internally.

Example:

WriteLn Bank.FindConsumable(ERSConsumable.FOOD);
Bank.CountPoints()
function TRSBank.CountPoints(Consumable: TRSConsumable): Int32;
Method used to count the points of the first dose/portion of a consumable found in bank. This prioritizes higher dosage visible ones first and returns only just that one.

Bank.WithdrawConsumableAmount()
function TRSBank.WithdrawConsumableAmount(consumableType: ERSConsumable): Int32;
function TRSBank.WithdrawConsumableAmount(consumableType: ERSConsumable; consumable: TRSConsumable): Int32; overload;
Method used to return the amount we need to withdraw to meet the TRSConsumable.MinInvPoints.

Bank.WithdrawConsumable()
function TRSBank.WithdrawConsumable(consumableType: ERSConsumable): Boolean;
Method used to withdraw a consumable type.

Example:

FoodHandler.MinInvPoints := 100;
Bank.WithdrawConsumable(ERSConsumable.FOOD); //This will withdraw FOODs until we have 100 points value of 