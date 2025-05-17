PortalNexus
Portal Nexus interface by Reldnahc.

TRSPortalNexus.ClickDestination
function TRSPortalNexus.ClickDestination(destination: ERSNexusDestination, useKeyboard : Boolean = False): Boolean;
function TRSPortalNexus.ClickDestination(destination: ERSNexusDestination; chance: Double = BioHash): Boolean; overload;
Finds the destination in the scroll area and clicks it.

Example:

 WriteLn TRSPortalNexus.ClickPortalDestination(ERSNexusDestination.FALADOR);
TRSPortalNexus.FindDestinations
function TRSPortalNexus.FindDestinations(out boxes: TBoxArray): TStringArray;
Returns the visible destinations in the portal nexus interface.

Example:

 WriteLn TRSPortalNexus.FindDestinations();
TRSPortalNexus.FindPortalDestination
function TRSPortalNexus.FindPortalDestination(destination: ERSNexusDestination; out b: TBox): Boolean;
function TRSPortalNexus.FindPortalDestination(destination: ERSNexusDestination): Boolean; overload;
Finds the destination specified in the portal nexus.

Example:

 WriteLn TRSPortalNexus.FindPortalDestination(ERSNexusDestination.FALADOR);