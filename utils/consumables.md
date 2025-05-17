Consumables
This file contains types and arrays of consumable items that can be used as is or by the consumable handlers in wasplib.

type ERSConsumable
ERSConsumable = (
  FOOD,
  PRAYER,
  POISON,
  ANTI_FIRE,
  STRENGTH_BOOST,
  ATTACK_BOOST,
  DEFENCE_BOOST,
  RANGING_BOOST,
  MAGIC_BOOST,
  BOOST,
  ENERGY
);
ERSConsumable is a enumerator that contains all types of consumable.

var CONSUMABLE_ARRAYS
var
  FOOD_ARRAY: TRSItemArray = ['Shrimps', 'Cooked chicken', 'Cooked meat', 'Sardine', 'Bread', 'Herring', 'Mackerel', 'Choc-ice', 'Trout', 'Cod', 'Pike', 'Roast beast meat', 'Pineapple punch', 'Salmon', 'Tuna', 'Jug of wine', 'Rainbow fish', 'Stew', 'Banana stew', 'Cake(1..3)', 'Meat pie(1..2)', 'Bass', 'Plain pizza(1..2)', 'Lobster', 'Swordfish', 'Potato with butter', 'Apple pie(1..2)', 'Chocolate cake(1..3)', 'Tangled toad' 's legs', 'Chocolate bomb', 'Potato with cheese', 'Meat pizza(1..2)', 'Admiral pie(1..2)', 'Monkfish', 'Anchovy pizza(1..2)', 'Cooked karambwan', 'Curry', 'Ugthanki kebab', 'Guthix rest(1..4)', 'Dragonfruit pie(1..2)', 'Mushroom potato', 'Shark', 'Sea turtle', 'Pineapple pizza(1..2)', 'Summer pie(1..2)', 'Wild pie(1..2)', 'Manta ray', 'Tuna potato', 'Dark crab', 'Anglerfish', 'Saradomin brew(1..4)'];
  PRAYER_ARRAY: TRSItemArray = ['Zamorak brew(1..4)', 'Sanfew serum(1..4)', 'Super restore(1..4)', 'Prayer potion(1..4)', 'Jangerberries'];
  ENERGY_ARRAY: TRSItemArray = ['White tree fruit', 'Winter sq' 'irkjuice', 'Spring sq' 'irkjuice', 'Autumn sq' 'irkjuice', 'Summer sq' 'irkjuice', 'Bandages', 'Guthix rest(1..4)', 'Papaya fruit', 'Energy potion(1..4)', 'Purple sweets', 'Summer pie(1..2)', 'Super energy(1..4)', 'Stamina potion(1..4)', 'Strange fruit', 'Mint cake', 'Gout tuber'];
  ANTI_POISON_ARRAY: TRSItemArray = ['Sanfew serum(1..4)', 'Anti-venom+(1..4)', 'Anti-venom(1..4)', 'Antidote++(1..4)', 'Antidote+(1..4)', 'Superantipoison(1..4)', 'Antipoison(1..4)',  'Extended anti-venom+(1..4)'];
  ANTI_FIRE_ARRAY: TRSItemArray = ['Antifire potion(1..4)', 'Super antifire potion(1..4)', 'Extended antifire(1..4)', 'Extended super antifire(1..4)'];
  BOOST_ARRAY: TRSItemArray = ['Divine super combat potion(1..4)', 'Super combat potion(1..4)', 'Divine bastion potion(1..4)', 'Bastion potion(1..4)', 'Divine battlemage potion(1..4)', 'Battlemage potion(1..4)'];
  STRENGTH_BOOST_ARRAY: TRSItemArray = ['Divine super strength potion(1..4)', 'Super strength(1..4)', 'Strength potion(1..4)'];
  ATTACK_BOOST_ARRAY: TRSItemArray = ['Divine super attack potion(1..4)', 'Super attack(1..4)', 'Attack potion(1..4)'];
  DEFENCE_BOOST_ARRAY: TRSItemArray = ['Divine super defence potion(1..4)', 'Super defence(1..4)', 'Defence potion(1..4)'];
  RANGING_BOOST_ARRAY: TRSItemArray = ['Divine ranging potion(1..4)', 'Ranging potion(1..4)'];
  MAGIC_BOOST_ARRAY: TRSItemArray = ['Divine magic potion(1..4)', 'Magic potion(1..4)'];
  TRASH_ARRAY: TRSItemArray = ['Cocktail glass', 'Jug', 'Bowl', 'Pie dish', 'Vial', 'Beer glass', 'Empty cup'];

  CONSUMABLE_ARRAYS: array [ERSConsumable] of TRSItemArray = [FOOD_ARRAY, PRAYER_ARRAY, ENERGY_ARRAY, ANTI_POISON_ARRAY, ANTI_VENOM_ARRAY, ANTI_FIRE_ARRAY, BOOST_ARRAY, STRENGTH_BOOST_ARRAY, ATTACK_BOOST_ARRAY, DEFENCE_BOOST_ARRAY, RANGING_BOOST_ARRAY, MAGIC_BOOST_ARRAY];
Global consumable arrays variables. These arrays holds all types of consumable for each respective purpose with the exception of TRASH_ARRAY which are possible left over items from consumables. They are in UPPERCASE because they are intended to be treated as constants but are variables in case the user whishes to modify them.

CONSUMABLE_ARRAYS is an array of all consumables. One can access a consumable array type easiely like so:

WriteLn CONSUMABLE_ARRAYS[ERSConsumable.ENERGY];
type TRSConsumable
TRSConsumable = record
  Item: TRSItem;
  Points: UInt32;
  Timer: UInt32;
  BankTab: Int32;
  Cost: Int32;
  IsSetup: Boolean;
end;
TRSConsumableArray = array of TRSConsumable;
TRSConsumable is the record used in all consumables. It contains base properties all consumables have.

type TRSConsumableType
type
  TRSFood = type TRSConsumable;
  TRSFoodArray = array of TRSFood;
  TRSPrayerPotion = type TRSConsumable;
  TRSPrayerPotionArray = array of TRSPrayerPotion;
  TRSEnergyBoost = type TRSConsumable;
  TRSEnergyBoostArray = array of TRSEnergyBoost;
  TRSBoost = record(TRSConsumable)
    Skills: array of ERSSkill;
    LevelsBoost: TIntegerArray;
    Countdown: TCountdown;
  end;
  TRSBoosArray = array of TRSBoost;
Types used in all consumables for each respective purpose. This includes food and certain potions. TRSBoost type of consumable has a timer to keep track when it lost it’s effect after being eaten/drank.

Consumable._Setup
procedure TRSConsumable._Setup();
Used internally by consumable handlers/managers to setup common things among all consumable records.

Consumable.Setup
procedure TRSConsumable.SetupFood();
procedure TRSConsumable.SetupPrayer();
procedure TRSConsumable.SetupEnergy();
procedure TRSConsumable.SetupAntiPoison();
procedure TRSConsumable.SetupAntiFire();
procedure TRSConsumable.SetupBoost();
Used internally by consumable handlers/managers to setup the consumable records.

ConsumableArray.Contains()
function TRSConsumableArray.Contains(Value: TRSItem): Boolean;
Wrapper method to check if a TRSConsumableArray has the specified TRSItem in one of it’s TRSConsumables.

ConsumableArray.Reversed()
function TRSConsumableArray.Reversed(): TRSConsumableArray;
Reverses the order of the TRSConsumableArray.

var TotalConsumableCost
Global TotalConsumableCost variable used to track the amount of money spent in by consuming consumables.
