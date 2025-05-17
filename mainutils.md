UTILS
UTILS -> DATA

Data
type TItemData
ItemData.SetupWikiPrices()
ItemData.GetData
ItemData.GetTradeableID
ItemData.GetPrice
ItemData.GetPriceInt
ItemData.GetAverage
ItemData.GetOSRSBoxInt()
ItemData.GetOSRSBoxBoolean()
ItemData.GetHighAlch()
ItemData.GetHighAlchProfit()
ItemData.GetLowAlchProfit()
type ERSAttackType
type TRSMonsterDrop
type TMonsterData
TMonsterData.Setup()
TMonsterData.GetInt()
TMonsterData.GetString()
TMonsterData.IsAgressive()
TMonsterData.GetJSONArray()
TMonsterData.GetJSONObject()
TMonsterData.GetAttackTypes()
TMonsterData.GetDrop()
TMonsterData.GetDrops()
type TWeaponData
WeaponData.Setup
WeaponData.GetInt
WeaponData.GetAttackType
WeaponData.IsTwoHanded
WeaponData.GetRequirementsJSON
type TGearData
GearData.Setup
GearData.GetJSONArray
GearData.GetItems
UTILS -> FORMS

Form Utilities
TControl.IsInitiated
TControl.Set
TControl.Get
TComponent.GetChild
TComponent.RemoveChildren
Component.NumberField
Component.TimeField
Component.NumberArrayField
Control.OpenLink
CustomEdit.IsEmpty
CustomEdit.GetIntegerArray
TControl.Create
TImage.LoadFromFile
TControl.LoadFromFile
TControl.SwapImage
TControl.GetTrueWidth
TControl.GetTrueHeight
CheckBox.SetChecked
CheckBox.IsChecked
CheckBox.Toggle
LabeledControl
TLabeledPanel
LabeledEdit
LabeledCheckBox
LabeledComboBox
LabeledListBox
LabeledMemo
LabeledTrackBar
CheckCheckGroup
LabeledControl.IsInitiated
TLabeledControl.Create
LabeledControl.SetCaption
LabeledControl.SetHint
LabeledControl.ShowHint
LabeledControl.SetShowHint
LabeledControl.SetTooltip
LabeledControl.SetName
LabeledControl.Set
LabeledControl.BringToFront
LabeledControl.Get
LabeledControl.SetText
LabeledControl.GetText
LabeledControl.GetName
LabeledControl.Clear
LabeledCheckBox.SetChecked
LabeledCheckBox.IsChecked
LabeledCheckBox.GetState
LabeledControl.SetEnabled
LabeledControl.SetPasswordChar
LabeledControl.SetMaxLength
LabeledControl.GetMaxLength
LabeledControl.SetStyle
LabeledControl.AddItem
LabeledControl.AddItemArray
LabeledControl.SetItemIndex
LabeledControl.GetItemIndex
ScriptForm
Compiler Directives
TScriptForm
CREDENTIALS_FILE
RewriteCredentials
TScriptForm.AddTab
TScriptForm.InsertTab
TScriptForm.GetTab
TScriptForm.SetTabOrder
TScriptForm.CreateTabs
TScriptForm.StartScript
TScriptForm.Setup
TScriptForm.Show
TScriptForm.Run
UTILS -> RECORDER

Recorder
type Recorder
Recorder.Start
UTILS -> INPUT

RemoteInput
Mouse
Mouse.Move
MouseZoom
type TRSMouseZoom
RSMouseZoom.GetNext
RSMouseZoom.Level2Slider
RSMouseZoom.Slider2Level
RSMouseZoom.Scroll
RSMouseZoom.MaxZoom
RSMouseZoom.MaxZoomBlind
RSMouseZoom.GetZoomLevel
RSMouseZoom.SetZoomLevel
RSMouseZoom.RunStressTest
RSMouseZoom.DrawGraph
var RSMouseZoom
UTILS

Misc
GetPackageVersion
Math
Double.GetDigit
NumberPerHour
String.Case
String.Is
Color
type SRLColors
GetNextCycleColor
RGB2BGR
RSCacheParser
type TRSCacheParser
RSCacheParser.Setup
RSCacheParser.GetPreference
RSCacheParser.Update
RSCacheParser.GetHexString
RSCacheParser.Print
RSCacheParser.GetOptionsAmount
RSCacheParser.RoofsHidden
RSCacheParser.TitleMusicDisabled
RSCacheParser.WindowMode
RSCacheParser.GetAuthenticatorAmount
RSCacheParser.GetAuthenticators
RSCacheParser.GetUsernameIndex
RSCacheParser.GetUsername
RSCacheParser.UsernameEndIndex
RSCacheParser.HideUsername
RSCacheParser.Brightness
RSCacheParser.MusicVolume
RSCacheParser.SoundEffectsVolume
RSCacheParser.AreaSoundVolume
RSCacheParser.Field1247
RSCacheParser.DisplayFPS
RSCacheParser.Field1238
Config
type TConfigJSON
TConfigJSON.GetConfig
TConfigJSON.Free
TConfigJSON.Setup
TConfigJSON.DeleteConfig
TConfigJSON.SaveConfig
TConfigJSON.Put
TConfigJSON.Has
TConfigJSON.Get
TConfigJSON.Remove
TConfigJSON.ToString
type TConfigINI
TConfigINI.Setup
TConfigINI.Put
TConfigINI.Get
TConfigINI.GetKeys
TConfigINI.Remove
TConfigINI.DeleteConfig
Utility types, contants and variables
type EWLBankLocation
Biometrics
GenerateUUIDV4
var BioHash
var BioHashOverride
type EBioBehavior
Antiban.SetupBiometrics
Antiban.GetBehavior
Antiban.GetChance
Antiban.GetMultiplier
Antiban.GetUniqueNumber
Antiban.GetUniqueAverage
Antiban.BioDice
Antiban.GetSleepHour
Antiban.GetSleepLength
Antiban.Wait
Antiban.Click
UTILS -> ITEMS

Items Extensions
TRSItem.Reorder
TRSItem.GetPortions
TRSItem.GetPortion
Item.GetArray
Item.GetSingle
Consumables
type ERSConsumable
var CONSUMABLE_ARRAYS
type TRSConsumable
type TRSConsumableType
Consumable._Setup
Consumable.Setup
ConsumableArray.Contains()
ConsumableArray.Reversed()
var TotalConsumableCost
UTILS -> HTTP

API
type APIClient
APICLient.SetUsername
APIClient.Setup
APIClient.GetUUID
APIClient.GetPassword
APIClient.GetUsername
APIClient.SetLocal
APIClient.HashPassword
APIClient.CheckPassword
APIClient.UpdatePassword
APIClient.CheckStats
APIClient.SubmitStats
APIClient.Pause
APIClient.Resume
APIClient.GetScript
APIClient.GetScriptRevision
APIClient.GetVersion
APIClient.GetAllVersions
HTTPClient
WaspClient
TWaspClient.CheckRoleAccess
TWaspClient.GetSubscriptions
TWaspClient.GetFreeAccess
tSubscriptionDataArray._MatchProduct
TWaspClient.GetProductCode
TWaspClient.GetProductLink
TWaspClient.ExplodeBundles
Authentication
TWaspClient.GetScriptInfo
TWaspClient.HasAccess
TWaspClient.CheckSubscription
UTILS -> GEOMETRY

Cuboids
TPoint
TPointArray
TPointArray.ToString
T2DPointArray.Connect