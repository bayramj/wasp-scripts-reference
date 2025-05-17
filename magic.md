Magic
Extends SRL’s TRSMagic.

Magic.SpellWasCast
function TRSMagic.SpellWasCast(spell: ERSSpell): Boolean;
Internal helper function to decide wether we cast a spell or not.

Magic.CastSpell
function TRSMagic.CastSpell(spell: ERSSpell): Boolean; override;
Overrides the existing SRL TRSMagic.CastSpell() for better cast detection with the usage of WaspLib’s TRSMagic.SpellWasCast().

Magic.GetFilterButton
function TRSMagic.GetFilterButton(): TRSButton;
Returns the filter button in the magic tab.

Example:

Debug([Magic.GetFilterButton()]);
Magic.FiltersIsOpen
function TRSMagic.FiltersIsOpen(): Boolean;
Returns true/false if the filters interface of the magic tab is open.

Example:

WriteLn Magic.FiltersIsOpen();
Magic.OpenFilters
function TRSMagic.OpenFilters(): Boolean;
Attempts to open the filters interface of the magic tab. Returns true on success.

Example:

WriteLn Magic.OpenFilters();
Magic.CloseFilters
function TRSMagic.CloseFilters(): Boolean;
Attempts to close the filters interface of the magic tab. Returns true on success.

Example:

WriteLn Magic.CloseFilters();
Magic.GetBookSpellCount
function TRSMagic.GetBookSpellCount(): Int32;
Returns the number of spells declared in SRL for the current spellbook.

Example:

WriteLn Magic.GetBookSpellCount();
Magic.CountSpells
function TRSMagic.CountSpells(): Int32;
Returns the number of spells that exist in your magic tab.

Example:

WriteLn Magic.CountSpells();
if Magic.GetBookSpellCount() <> Magic.CountSpells() then
  WriteLn 'Something is wrong!';
Magic.GetFilterButtons
function TRSMagic.GetFilterButtons(): TRSButtonArray;
Returns the buttons of the magic tab filter interface.

Example:

Debug(Magic.GetFilterButtons());
Magic.IsFiltered
function TRSMagic.IsFiltered(): Boolean;
Returns wether the spells are currently filtered or not. Can work with the filter interface open or closed as long as the magic tab is open.

Example:

WriteLn Magic.IsFiltered();
Magic.DisableFilters
function TRSMagic.DisableFilters(): Boolean;
Attempts to disable magic spell filters.

Example:

WriteLn Magic.DisableFilters();