Optional Files
To include all optional files add the following to your script after WaspLib:

{$I WaspLib/optional.simba}
Note 


OPTIONAL -> INTERFACES -> MAINSCREEN

FurnitureBuilder
FurnitureBuilder.IsOpen
FurnitureBuilder.Setup
FurnitureBuilder.Close
var FurnitureBuilder
SilverScreen
SilverScreen.IsOpen
SilverScreen.Close
SilverScreen.SetQuantity
SilverScreen.CanCraftItem
SilverScreen.IsItemHighlighted
SilverScreen.CraftItem
var SilverScreen
CraftScreen
CraftScreen.IsOpen
CraftScreen.Close
CraftScreen.SetQuantity
CraftScreen.CanCraftItem
CraftScreen.IsItemHighlighted
CraftScreen.CraftItem
DriftNet
TRSDriftNet.BankOverlayOpen
TRSDriftNet.DestroyOverlayOpen
TRSDriftNet.HasOverlay
TRSDriftNet.GetSlotBoxes
TRSDriftNet.GetButtons
TRSDriftNet.GetButton
Anvil
Anvil.GetSlots
Anvil.Setup
Anvil.IsOpen
Anvil.Close
var Anvil
PortalNexus
TRSPortalNexus.ClickDestination
TRSPortalNexus.FindDestinations
TRSPortalNexus.FindPortalDestination
FairyRing
FairyRing.Setup
FairyRing.IsOpen
FairyRing.Close
FairyRing.HandleItem
FairyRing.Open
FairyRing.WalkOpen
FairyRing.IsLetterValid
FairyRing.IsCodeValid
FairyRing.GetLetterBox
FairyRing.GetLetter
FairyRing.GetCurrentCode
FairyRing.GetRotationBox
FairyRing.Spin
FairyRing.SetDial
FairyRing.DialCode
FairyRing.GetTeleportButton
FairyRing.ClickTeleportButton
FairyRing.GetLogCodes
FairyRing.FindLogCode
FairyRing.ClickLogCode
FairyRing.HandleInterface
FairyRing.Teleport
FairyRing.WalkTeleport
var FairyRing
Lectern
OPTIONAL -> HANDLERS

LootHandler
CombatHandler
TRSFishingHandler
TRSFishingHandler.Setup
TRSFishingHandler.Reset
TRSFishingHandler.GetMMShoreLine
TRSFishingHandler.GetMSShoreLine
TRSFishingHandler.FindWaterDirection
TRSFishingHandler.FindSpot
TRSFishingHandler.WaitSpot
TRSFishingHandler.SpotMoved
TRSFishingHandler._StoppedFishing
TRSFishingHandler.CheckFishing
TRSFishingHandler.FacingWater
TRSFishingHandler.ClickSpot
POH Handler
PRSWalker
type TRSPOHHandler
POH.Init()
POH.GetAdjacentRooms()
TRSPOHHandler.GetRoomCoordinate()
POH.GetCuboid()
POH.ContainsObject()
POH.MapRoomObjects()
POH.MapAdjacentRooms()
POH.Setup()
POH.LoadSuroundings()
POH.Position()
POH.DebugPosition()
POH.GetCurrentRoom()
POH Objects
POH.Find
TRSPOHHandler.Draw()
POH.Interact
POH.WalkInteract
var POH
Debug
RoomObjects
ERSRoomObject
TRoomObject
TRoomObject.Init()
TRoomObject.Setup()
TRoomObject.AddCoordinates()
TRoomObject.Find
TRoomObject.Draw
TRoomObject.Interact
POHMap
type ERSHouseRoom
type TPOHMap
TPOHMap.Free()
TPOHMap.Init()
TPOHMap.GetRoomBitmapBox()
TPOHMap.GetRoomBitmap()
TPOHMap.RotateBitmap()
TPOHMap.WriteRoom()
TPOHMap.ReadRoom()
TPOHMap.PrintRooms()
TPOHMap.DrawMap()
TPOHMap.GetPointIndex()
TPOHMap.GetRoom()
TPOHMap.GetRoomTopLeft()
TPOHMap.GetAdjacentIndices()
TPOHMap.SampleSearch()
Discord
type TDiscordEmbed
type TDiscordWebhook
type TDiscordClient
TDiscordWebhook.Setup
TDiscordWebhook.AddEmbed
TDiscordWebhook.ClearEmbeds
TDiscordWebhook.ClearAll
TDiscordWebhook.ToJSON
TDiscordClient.Setup
TDiscordClient.SetWebhook
TDiscordClient.SetUsername
TDiscordClient.SetAvatar
TDiscordClient.Send
TDiscordClient.SendFile
TDiscordClient.SendScreenshot
TDiscordClient.MentionUser
TDiscordClient.Free
OPTIONAL -> HANDLERS -> HOUSE

HouseMap
type EHouseLocation
type EHouseDecoration
type EHouseRoom
type EHouseObject
type EHouseTeleport
HouseMap
type THouseLoader
THouseLoader.Free()
THouseLoader.Init()
THouseLoader.GetRoomBitmapBox()
THouseLoader.GetRoomBitmap()
THouseLoader.WriteRoom()
THouseLoader.ReadRoom()
THouseLoader.PrintRooms()
THouseLoader.DrawMap()
POH Handler
type THouseHandler
POH.Setup()
House.ScaledSearch
House.FullSearch
House.Position
House.DebugPosition
var House