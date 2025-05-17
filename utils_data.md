Data
Methods to fetch osrs data. This file has methods to fetch information about items, monsters and weapons.

type TItemData
TItemData = record(TSRLBaseRecord)
  ITEMS_ZIP: String;
  ITEMS_PATH: String;

  Client: THTTPClient;

  PriceData: TJSONObject;
  Definitions: TJSONArray;
  ReloadTimer: TCountDown;
  IsSetup, OSRSBoxIsSetup, Disabled: Boolean;
end;
TItemData type, responsible to handle anything that is related to item data.

ItemData.SetupWikiPrices()
procedure TItemData.SetupPrices();
Internal method called automatically when we require price data. Doesn’t need to be called since it will be called automatically if ItemData.WikiPriceIsSetup is false. It’s also recalled when we try to fetch item data and 20 minutes have passed to update prices.

ItemData.GetData
function ItemData.GetData(Item: String): TJSONObject;
Internal method used to retrieve a TJSONObject of the Item we want information on. Item should be an item ID.

ItemData.GetTradeableID
function ItemData.GetTradeableID(Item: TRSItem): String;
Internal method used to retrieve only the tradeable version of an item if it exists. Some items have versions of themselves that are not tradeable and can’t be used to fetch item prices, such as degraded items, ornamented items, etc.

ItemData.GetPrice
function ItemData.GetPrice(Item: TRSItem): TJSONObject;
Internal method used to fetch a price data TJSONObject of a certain item.

ItemData.GetPriceInt
function ItemData.GetPriceInt(Item: TRSItem; Key: String): Int32;
Wrapper method used to fetch ints from ItemData.GetPrice(). To use this you should be familar with the structure of the JSONObject ItemData.GetPrice() returns.

Example:

WriteLn ItemData.GetPriceInt('Abyssal whip', 'low'); // will print the low price of abyssal whip.
WriteLn ItemData.GetPriceInt('Abyssal whip', 'high'); // will print the high price of abyssal whip.
ItemData.GetAverage
function ItemData.GetAverage(Item: TRSItem): Int32;
Method used to get the average price of Item.

Example:

WriteLn ItemData.GetAverage('Abyssal whip');
ItemData.GetOSRSBoxInt()
function ItemData.GetOSRSBoxInt(Item: TRSItem; Key: String): Int32;
Wrapper method used to get the integer values of the OSRSBox item json. To use it, knowledge about the file structure is required.

Example:

WriteLn ItemData.GetOSRSBoxInt('Abyssal whip', 'highalch'); //will print high alch value for the abyssal whip.
ItemData.GetOSRSBoxBoolean()
function ItemData.GetOSRSBoxBoolean(Item: TRSItem; Key: String): Boolean;
Wrapper method used to get the boolean values of the OSRSBox item json. To use it, knowledge about the file structure is required.

Example:

WriteLn ItemData.GetOSRSBoxBoolean('Abyssal whip', 'tradeable_on_ge');
ItemData.GetHighAlch()
function ItemData.GetHighAlch(Item: TRSItem): Int32;
Method used to get the the high alchemy value of an item.

Example:

WriteLn ItemData.GetHighAlch('Magic longbow');
ItemData.GetHighAlchProfit()
function ItemData.GetHighAlchProfit(Item: TRSItem): Int32;
Method used to get the the high alchemy profit of an item.

Note

HighAlchProfit = HighAlchValue - ItemAveragePrice - NatureRuneAveragePrice

Example:

WriteLn ItemData.GetHighAlchProfit('Magic longbow');
ItemData.GetLowAlchProfit()
function ItemData.GetLowAlchProfit(Item: TRSItem): Int32;
Method used to get the the low alchemy profit of an item.

Note

LowAlchProfit = LowAlchValue - ItemAveragePrice - NatureRuneAveragePrice

Example:

WriteLn ItemData.GetLowAlchProfit('Magic longbow');
type ERSAttackType
ERSAttackType = (MELEE_ATTACK_TYPE, RANGED_ATTACK_TYPE, MAGIC_ATTACK_TYPE, TYPELESS_ATTACK_TYPE);
Enum of Attack types in game. Can be used to know what to pray for example.

type TRSMonsterDrop
type
  TRSMonsterDrop = record
    Item: String;
    ID: String;
    Stackable: Boolean;
    Noted: Boolean;
    Quantity: Int32;
  end;
  TRSMonsterDropArray = array of TRSMonsterDrop;
Helper record to handle monster drops. Has several variable that hold information about monster drops such as wether it’s stackable and/or noted and quantity.

type TMonsterData
TMonsterData = record(TSRLBaseRecord)
  MONSTERS_ZIP: String;
  CACHE_PATH: String;

  Names: TStringList;
  Data: TJSONArray;
  IsSetup: Boolean;
end;
Static TMonsterData type, responsible to handle anything that is related to monsters data.

TMonsterData.Setup()
procedure TMonsterData.Setup();
Internal method to setup the TMonsterData record.

TMonsterData.GetInt()
function TMonsterData.GetInt(Monster, Key: String): Int32;
Wrapper method to get integer data from from monsters.json.

Note

Using this requires you to know the structure of the monster.json file.

Example:

WriteLn TMonsterData.GetInt('Cow', 'hitpoints'); //This will print 8.
TMonsterData.GetString()
function TMonsterData.GetString(Monster, Key: String): String;
Wrapper method to get string data from monsters.json.

Note

Using this requires you to know the structure of the monster.json file.

Example:

WriteLn TMonsterData.GetString('Cow', 'drops');
TMonsterData.IsAgressive()
function TMonsterData.IsAgressive(Monster): String;
Method to get information on wether a monster is aggressive or not.

Example:

WriteLn TMonsterData.IsAgressive('Cow'); //Will print False.
TMonsterData.GetJSONArray()
function TMonsterData.GetJSONArray(Monster, Key: String): TJSONArray;
Internal method to get a TJSONArray value from monsters.json.

TMonsterData.GetJSONObject()
function TMonsterData.GetJSONObject(Monster, Key: String): TJSONObject;
Internal method to get a TJSONObject value from monsters.json.

TMonsterData.GetAttackTypes()
function TMonsterData.GetAttackTypes(Monster: String): array of ERSAttackType;
Method used to get an array of ERSAttackType used by the specified monster.

TMonsterData.GetDrop()
function TMonsterData.GetDrop(DropJSON: TJSONObject): TRSMonsterDrop;
Method to convert a monster json object to a TRSMonsterDrop.

TMonsterData.GetDrops()
function TMonsterData.GetDrops(Monster: String): TRSMonsterDropArray;
Method to return all monster drops as an array of TRSMonsterDrop.

Example:

WriteLn TMonsterData.GetDrops('Abyssal demon'); //prints all monster drops.
type TWeaponData
type
  TWeaponData = record
    Data: TJSONObject;
    IsSetup: Boolean;
  end;
Type responsible of handling anything that is related to weapons data.

WeaponData.Setup
procedure TWeaponData.Setup();
Internal method to setup TWeaponData.

WeaponData.GetInt
function TWeaponData.GetInt(weapon, key: String): Int32;
Method to fetch integer data from weapons.json.

Note

Using this requires knowledge of the structure of weapons.json

Example:

WriteLn TWeaponData.GetInt('Abyssal whip', 'special_attack'); //This will print 50.
WeaponData.GetAttackType
function TWeaponData.GetAttackType(weapon: String): ERSAttackType;
Returns the ERSAttackType of the weapon specified.

Example:

WriteLn TWeaponData.GetAttackType('Abyssal whip'); //This will print MELEE_ATTACK_TYPE.
WeaponData.IsTwoHanded
function TWeaponData.IsTwoHanded(weapon: String): Boolean;
Returns wether the weapon is two-handed or not.

Example:

WriteLn TWeaponData.IsTwoHanded('Abyssal whip'); //This will print false.
WeaponData.GetRequirementsJSON
function TWeaponData.GetRequirementsJSON(weapon: String): TJSONObject;
Returns a TJSONObject of the level requirements for the weapon.

type TGearData
type
  TGearData = record
    Data: TJSONObject;
    IsSetup: Boolean;
  end;
Type responsible of handling anything that is related to weapons data.

GearData.Setup
procedure TGearData.Setup();
Internal method to setup TGearData.

GearData.GetJSONArray
function TGearData.GetJSONArray(key: String): TJSONArray;
Method to fetch json arrays from gear.json.

Note

Using this requires knowledge of the structure of gear.json

GearData.GetItems
function TGearData.GetItems(key: String): TRSItemArray;
function TGearData.GetItems(slot: ERSEquipmentSlot): TRSItemArray; overload;
Method to fetch items under a key in gear.json.