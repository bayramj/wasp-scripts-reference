Form Utilities
Forms and components extensions.

This files contains custom components and methods to be used in forms.

TControl.IsInitiated
function TControl.IsInitiated(): Boolean;
Checks if the control has already been initiated.

TControl.Set
procedure TControl.SetTooltip(value: String);
procedure TControl.SetFontColor(value: Int32);
procedure TControl.SetChildsFontColor(value: Int32);
TControl.Set methods. Their names are self explanatory.

For some reason TControl.SetHint cannot be overriden, so a custom method for this was made.

TControl.Get
function TControl.GetRight(): Int32;
function TControl.GetBottom(): Int32;
TControl.Get methods. Their names are self explanatory.

TComponent.GetChild
function TComponent.GetChild(name: TComponentName): TComponent;
Recursively search for a children with the specified name.

TComponent.RemoveChildren
procedure TComponent.RemoveChildren(release: Boolean = False);
Recursively remove children from a parent. To also free the parent set release to true. All children are freed when using this.

Component.NumberField
procedure TComponent.NumberField(sender: TObject; var key: char);
Callback method to limit user input to numbers only and backspace. This numbers can be Ints or Doubles.

Component.TimeField
procedure TComponent.TimeField(sender: TObject; var key: char);
Callback method to limit user input to numbers only, backspace and a few characters used in time.

Component.NumberArrayField
procedure TComponent.NumberArrayField(sender: TObject; var key: char);
Callback method to limit user input to a TIntegerArray.

Control.OpenLink
procedure TControl.OpenLink(sender: TObject);
Open the link in the control caption.

CustomEdit.IsEmpty
function TCustomEdit.IsEmpty(): Boolean;
Returns true or false if the TCustomEdit (TEdit and TMemo) are empty.

CustomEdit.GetIntegerArray
function TCustomEdit.GetIntegerArray(): TIntegerArray;
Returns the TIntegerArray in the TCustomEdit (TEdit and TMemo). It’s probably a good idea to limit the TCustomEdit input with TComponent.IntArrayField().

TControl.Create
procedure TPanel.Create(owner: TControl);
procedure TPageControl.Create(owner: TControl);
procedure TTabSheet.Create(owner: TControl);
procedure TImage.Create(owner: TControl);
procedure TLabel.Create(owner: TControl);
procedure TEdit.Create(owner: TControl);
procedure TButton.Create(owner: TControl);
procedure TCheckBox.Create(owner: TControl);
procedure TRadioButton.Create(owner: TControl);
procedure TComboBox.Create(owner: TControl);
procedure TListBox.Create(owner: TControl);
procedure TMemo.Create(owner: TControl);
procedure TTrackBar.Create(owner: TControl);
TControl.Init() and TControl.SetParent() in a single method. Since this is something that has to be done almost always this wrapper was made.

TImage.LoadFromFile
procedure TImage.LoadFromFile(path: String);
Load a image file to a TImage directly.

TControl.LoadFromFile
procedure TControl.LoadFromFile(path: String);
Load a image file and set it as the background for a TControl. This can be used to set images for TPanels, TPageControls, TTabSheet, TButtons, etc.

TControl.SwapImage
procedure TControl.SwapImage(path: String);
Load a new image file and set it as the new background for a TControl. This can be used to swap images for TPanels, TPageControls, TTabSheet, TButtons, etc. If the TControl doesn’t have an image yet, this will also set it up.

TControl.GetTrueWidth
function TControl.GetTrueWidth(): Int32;
Get the true width of the TControl caption.

TControl.GetTrueHeight
function TControl.GetTrueHeight(): Int32;
Get the true height of the TControl caption.

CheckBox.SetChecked
procedure TCheckBox.SetChecked(value: Boolean);
Sets the checkbox checked or unchecked with a boolean.

CheckBox.IsChecked
function TCheckBox.IsChecked(): Boolean;
Gets the checkbox state, checked or unchecked with a boolean.

CheckBox.Toggle
procedure TCheckBox.Toggle();
Inverts the checkbox.

LabeledControl
type
  TLabeledControl = record
    Panel: TPanel;
    Caption: TLabel;
  end;
TLabeledControl is the base type for custom TLabeledControls. It’s not really meant to be used directly. If for some reason you need to see the control bounds, it’s recommended to set the panel bevel width to 1.

Changing TLabeledControl subcomponents align value can mess the position of everything.

TLabeledPanel
TLabeledPanel = type TLabeledControl;
Same exact thing as a TLabeledControl but with the purpose of being a panel for other components.

LabeledEdit
type
  TLabeledEdit = record(TLabeledControl)
    Edit: TEdit;
  end;
TLabeledEdit is, as the name implies a TEdit with a TLabel on top. Both components are contained in the TPanel inherited from TLabeledControl.

LabeledCheckBox
type TLabeledCheckBox = record(TLabeledControl)
CheckBox: TEdit;
end;
TLabeledCheckBox is, as the name implies a TCheckBox with a TLabel to it’s right. Both components are contained in the TPanel inherited from TLabeledControl.

Note

The standard TCheckBox already has a label by it but it’s hard to customize it.

LabeledComboBox
type
  TLabeledComboBox = record(TLabeledControl)
    ComboBox: TComboBox;
  end;
TLabeledComboBox is, as the name implies a TComboBox with a TLabel on top. Both components are contained in the TPanel inherited from TLabeledControl.

LabeledListBox
type
  TLabeledListBox = record(TLabeledControl)
    ListBox: TListBox;
  end;
TLabeledListBox is, as the name implies a TListBox with a TLabel on top. Both components are contained in the TPanel inherited from TLabeledControl.

LabeledMemo
type
  TLabeledMemo = record(TLabeledControl)
    Memo: TMemo;
  end;
TLabeledMemo is, as the name implies a TMemo with a TLabel on top. Both components are contained in the TPanel inherited from TLabeledControl.

LabeledTrackBar
type
  TLabeledTrackBar = record(TLabeledControl)
    TrackBar: TTrackBar;
  end;
TLabeledTrackBar is, as the name implies a TTrackBar with a TLabel on top. Both components are contained in the TPanel inherited from TLabeledControl.

CheckCheckGroup
type
  TCheckCheckGroup = record(TLabeledCheckBox)
    CaptionPanel, GroupPanel: TPanel;
    Group: array of TLabeledCheckBox;
  end;
TCheckCheckGroup is, a custom component. The best way to describe it is a TLabeledCheckBox group that the caption itself is a checkbox to enable/disable the whole group.

LabeledControl.IsInitiated
function TLabeledControl.IsInitiated(): Boolean;
Checks if the custom labeled control has already been initiated.

TLabeledControl.Create
procedure TLabeledControl.Create(owner: TControl);
procedure TLabeledPanel.Create(owner: TControl); override;
procedure TLabeledEdit.Create(owner: TControl); override;
procedure TLabeledCheckBox.Create(owner: TControl); override;
procedure TLabeledComboBox.Create(owner: TControl); override;
procedure TLabeledListBox.Create(owner: TControl); override;
procedure TLabeledMemo.Create(owner: TControl); override;
procedure TLabeledTrackBar.Create(owner: TControl); override;
Custom components TLabeledControl.Init() and TLabeledControl.SetParent() in a single method. Since this is used very often a wrapper was made.

LabeledControl.SetCaption
procedure TLabeledControl.SetCaption(value: String);
Set the labeled control caption.

LabeledControl.SetHint
procedure TLabeledControl.SetHint(value: String);
Set the labeled control hint (tooltip).

LabeledControl.ShowHint
procedure TLabeledControl.ShowHint();
Sets show hint (tooltip) to true.

LabeledControl.SetShowHint
procedure TLabeledControl.SetShowHint(value: Boolean);
Sets show hint (tooltip) to true or false.

LabeledControl.SetTooltip
procedure TLabeledControl.SetTooltip(value: String);
Same as the previous one but makes sure that .ShowHint() is enabled if value was not empty. For more info read about TControl.SetTooltip().

LabeledControl.SetName
procedure TLabeledEdit.SetName(value: String);
procedure TLabeledCheckBox.SetName(value: String);
procedure TLabeledComboBox.SetName(value: String)
procedure TLabeledListBox.SetName(value: String);
procedure TLabeledMemo.SetName(value: String);
procedure TLabeledTrackBar.SetName(value: String);
Sets names to the subcomponents of the TLabeledControl. Caption is named with value + ‘_caption’ while the other component is appended with it’s name.

LabeledControl.Set
procedure TLabeledControl.SetLeft(value: Int32);
procedure TLabeledControl.SetTop(value: Int32);
procedure TLabeledControl.SetWidth(value: Int32);
procedure TLabeledControl.SetHeight(value: Int32);
procedure TLabeledControl.SetAlign(value: TAlign);
procedure TLabeledControl.SetColor(value: Int32);
procedure TLabeledControl.SetFontColor(color: TColor);
procedure TLabeledControl.SetFontSize(size: Int32);
procedure TLabeledControl.SetVisible(value: Boolean);
TLabeledControl Set methods. The methods are self explanatory. The only thing that should be kept in mind is that they only interactwith the TLabeledControl.Panel.

LabeledControl.BringToFront
procedure TLabeledControl.BringToFront();
Brings the control to front.

LabeledControl.Get
function TLabeledControl.GetLeft(): Int32;
function TLabeledControl.GetTop(): Int32;
function TLabeledControl.GetRight(): Int32;
function TLabeledControl.GetBottom(): Int32;
function TLabeledControl.GetHeight(): Int32;
function TLabeledControl.GetVisible(): Boolean;
TLabeledControl Get methods. The methods are self explanatory.

LabeledControl.SetText
procedure TLabeledEdit.SetText(value: String);
procedure TLabeledComboBox.SetText(value: String);
procedure TLabeledMemo.SetText(value: String);
Sets the visible text in the TLabeledControl to value.

LabeledControl.GetText
function TLabeledEdit.GetText(): String;
function TLabeledComboBox.GetText(): String;
function TLabeledListBox.GetText(): String;
function TLabeledMemo.GetText(): String;
Gets the visible or selected text in the TLabeledControl.

Example:

WriteLn myEdit.GetText();
LabeledControl.GetName
function TLabeledControl.GetName(): String;
Gets the TLabeledControl name.

LabeledControl.Clear
procedure TLabeledEdit.Clear();
procedure TLabeledComboBox.Clear();
procedure TLabeledListBox.Clear();
procedure TLabeledMemo.Clear();
Clears the TLabeledControl.

LabeledCheckBox.SetChecked
procedure TLabeledCheckBox.SetChecked(value: Boolean);
Sets the checkbox or not depending on value.

LabeledCheckBox.IsChecked
function TLabeledCheckBox.IsChecked(): Boolean;
Gets the checkbox state true or false.

LabeledCheckBox.GetState
function TLabeledCheckBox.GetState(): TCheckBoxState;
Gets the checkbox state.

LabeledControl.SetEnabled
procedure TLabeledEdit.SetEnabled(value: Boolean);
procedure TLabeledCheckBox.SetChecked(value: Boolean);
procedure TLabeledComboBox.SetEnabled(value: Boolean);
procedure TLabeledListBox.SetEnabled(value: Boolean);
procedure TLabeledMemo.SetEnabled(value: Boolean);
Sets the checkbox or not depending on value.

LabeledControl.SetPasswordChar
procedure TLabeledEdit.SetPasswordChar(value: Char = '*');
procedure TLabeledMemo.SetPasswordChar(value: Char = '*');
Sets the TLabeledControl to hide the displayed text with value characters. Mostly used to hide passwords.

LabeledControl.SetMaxLength
procedure TLabeledEdit.SetMaxLength(value: Int32);
procedure TLabeledMemo.SetMaxLength(value: Int32);
Sets the maximum length of characters accepted by the TLabeledControl.

LabeledControl.GetMaxLength
function TLabeledEdit.GetMaxLength(): Int32;
function TLabeledMemo.GetMaxLength(): Int32;
Returns the maximum length of characters accepted by the TLabeledControl.

LabeledControl.SetStyle
procedure TLabeledComboBox.SetStyle(value: TComboBoxStyle);
procedure TLabeledListBox.SetStyle(value: TListBoxStyle);
Sets the TLabeledControl style.

LabeledControl.AddItem
procedure TLabeledCombobox.AddItem(value: String);
procedure TLabeledListBox.AddItem(value: String);
Adds an item to the TLabeledControl.

LabeledControl.AddItemArray
procedure TLabeledCombobox.AddItemArray(valueArray: TStringArray);
procedure TLabeledListBox.AddItemArray(valueArray: TStringArray);
procedure TCheckCheckGroup.AddItemArray(valueArray: TStringArray);
Adds an array of items to the TLabeledControl.

LabeledControl.SetItemIndex
procedure TLabeledCombobox.SetItemIndex(value: Int32);
procedure TLabeledListBox.SetItemIndex(value: Int32);
Sets the selected index for the TLabeledControl.

LabeledControl.GetItemIndex
function TLabeledCombobox.GetItemIndex(): Int32;
function TLabeledListBox.GetItemIndex(): Int32;
Gets the selected index of the TLabeledControl.