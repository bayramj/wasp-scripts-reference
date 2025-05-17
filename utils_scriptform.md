ScriptForm
This file is responsible for creating and managing WaspLib’s forms.

This might be complicated to understand if you are not familiar with pointers and type casting because it heavily relies on both.

Compiler Directives
{$IFHASFILE credentials.simba}{$I credentials.simba}{$ENDIF}
{$IFNDEF SCRIPT_ID}{$DEFINE SCRIPT_ID := ''}{$ENDIF}
{$IFNDEF SCRIPT_REVISION}{$DEFINE SCRIPT_REVISION := ''}{$ENDIF}
The first line looks for a credentials.simba file and include it if it exists. This is what gives WaspLib scripts access to their accounts through several scripts. It’s important to know that player information is stored in Simba code to compile when the file is included, what this means is that the information is in plain text.

The next 2 lines are unrelated to credentials but related to each other. The way TScriptForm was made, it assumes a valid SCRIPT_ID and SCRIPT_REVISION have been assigned. Because WaspLib is not meant to enforce the usage of https://waspscripts..com, this was added as a way of users being able to use WaspLib regardless of having a script id/revision or not.

TScriptForm
TScriptForm = record
Size: TPoint;
PageControl: TPageControl;
Tabs: array of TTabSheet;
Start: TButton;
Form: TForm;
end;
TScriptForm is the record responsible for handling the WaspLib form.

CREDENTIALS_FILE
..pascal:: const CREDENTIALS_FILE = AppPath + ‘credentials.simba’;

Global constant that points to the location of credentials.simba which is Simba’s root directory.

RewriteCredentials
procedure RewriteCredentials();
Internal method used to rewrite the credentials.simba file. This will use whatever is stored at the moment in Login.Players array and replace Simba/credentials.simba with it written in the appropiate format.

Example:

begin
  Login.AddPlayer('USERNAME1', 'PASSWORD1', 'PIN1', []); //[] is an array of world numbers.
  Login.AddPlayer('USERNAME2', 'PASSWORD2', 'PIN2', []);
  Login.AddPlayer('USERNAME3', 'PASSWORD3', 'PIN3', []);
end;
TScriptForm.AddTab
procedure TScriptForm.AddTab(caption: String);
procedure TScriptForm.AddTab(tab: TTabSheet); overload;
procedure TScriptForm.AddTabArray(captions: TStringArray);
Methods to add tabs to TScriptForm.

When you a tab by caption be it a single one or an array of them, the caption you use can be used to reference the tab later.

It’s caption get sanitized with:

LowerCase(StringReplace(caption, ' ', '_', [rfReplaceAll]))
Which means that if you “HelLo WOrLD” as your caption, it’s name internally will become “hello_world_settings”. This is only important if you need to retrieve the tab with the use of Self.Form.GetChild(). If you use the other tab methods you simply have to write the caption name the same way you did the first time. Your tab will also be added to TScriptForm.Tabs as the last element of the array and you can get it right after adding it with MyForm.Tabs[High(MyForm.Tabs)].

This example as a very simple setup of a TScriptForm with one tab:

Example:

procedure TMyScriptForm.Run(); override;
var
  tab: TTabSheet;
begin
  Self.Setup('HELLO WORLD SCRIPT');
  Self.Start.setOnClick(@Self.StartScript);

  Self.AddTab('Script Settings');
  tab := Self.Tabs[High(Self.Tabs)];

  inherited;
end;
TScriptForm.InsertTab
procedure TScriptForm.InsertTab(caption: String; index: Int32 = 0);
procedure TScriptForm.InsertTab(tab: TTabSheet; index: Int32 = 0); overload;
Adds a tab to TScriptForm and places it in TScriptForm.Tabs at the specified index. This is rarely ever useful at all to be honest.

TScriptForm.GetTab
function TScriptForm.GetTab(index: Int32): TTabSheet;
function TScriptForm.GetTab(caption: String; ignoreCase: Boolean = False): TTabSheet; overload;
Returns a tab based on index or caption.

Example:

MyForm.AddTab('Hello wolrd');
tab := MyForm.GetTab('Hello world');
TScriptForm.SetTabOrder
procedure TScriptForm.SetTabOrder(captions: TStringArray; ignoreCase: Boolean = False); overload;
Changes the tab order to that of the specified captions in the TScriptForm.Tabs array. Keep in mind this doesnt actually move the tabs in the Form.

TScriptForm.CreateTabs
function TScriptForm.CreateAPISettings(): TTabSheet;
function TScriptForm.CreateAccountManager(owner: TControl): TPanel;
function TScriptForm.CreateAccountManager(): TTabSheet; overload;
function TScriptForm.CreateAntibanManager(): TTabSheet;
function TScriptForm.CreateConsumableSettings(owner: TControl; consumableType: ERSConsumable; addInfo: Boolean = True): TPanel;
function TScriptForm.CreateConsumableSettings(consumableType: ERSConsumable): TTabSheet; overload;
function TScriptForm.CreateBankSettings(): TTabSheet;
function TScriptForm.CreateLimitSettings(owner: TControl): TPanel;
function TScriptForm.CreateLimitSettings(owner: TControl): TPanel;
function TScriptForm.CreateRemoteInputSettings(owner: TControl): TPanel;
function TScriptForm.CreateVideoPanel(owner: TControl): TPanel;
function TScriptForm.CreateWaspLibSettings(limits: Boolean = True): TTabSheet;
function TScriptForm.CreateVersionPanel(owner: TControl; colors: TIntegerArray = [$27BA70, $00D8FF, $0000FF]; align: TAlign = alBottom): TPanel;
Set of methods used to create pre-configured panels and/or tabs to interact with SRL/WaspLib. The methods that return panels require you to specify a owner which will be the parent of that TPanel. Some panels might also require you to position the panel correctly as you wish. You can either align it or set coordinates.

All of this are quite complex but have all their own methods self contained and it’s not worth going over them since if you understand them, you might as well just refer to their source code anyway.

Very basic example of a full TScriptForm setup:

Example:

{$I SRL-T/osr.simba}
{$I WaspLib/osr.simba}

type
  TMyScriptForm = record(TScriptForm)
    Selector: TLabeledCombobox;
    Info: TLabel;
  end;

procedure TMyScriptForm.StartScript(sender: TObject); override;
begin
  //Read your form options to setup the script here.
  inherited; //This is important if you use TScript.Setup().
end;

procedure TMyScriptForm.Run(); override;
var
  tab: TTabSheet;
begin
  Self.Setup('HELLO WORLD SCRIPT');
  Self.Start.setOnClick(@Self.StartScript); //this is important, don't forget it.

  Self.AddTab('Script Settings');
  tab := Self.Tabs[High(Self.Tabs)];

  Self.CreateAccountManager(tab);

  with Self.Selector do
  begin
    Create(tab);
    SetCaption('Item type:');
    SetLeft(TControl.AdjustToDPI(40));
    SetTop(TControl.AdjustToDPI(170));
    SetStyle(csDropDownList);
    AddItemArray(['Item1', 'Item2', 'Item3', 'Item4']);
    SetItemIndex(2);
  end;

  with Self.Info do
  begin
    Create(tab);
    SetCaption('Get 99 Hello world today!');
    SetLeft(Self.Selector.GetRight() + TControl.AdjustToDPI(40));
    SetTop(TControl.AdjustToDPI(190));
  end;

  Self.CreateVersionPanel(tab);
  Self.CreateAntibanManager();
  Self.CreateBankSettings();
  Self.CreateWaspLibSettings();
  Self.CreateAPISettings();

  inherited;
end;

var
  MyScriptForm: TMyScriptForm;

begin
  MyScriptForm.Run();
  //RUN SCRIPT HERE!
end.
TScriptForm.StartScript
procedure TScriptForm.StartScript(sender: TObject);
This exists so you can close and terminate your script by closing the form window, otherwise it would just run the script. Overriding this will require you to use inherited on your override.

Overriding this is also my recommended way of setting up your script variables like the following example:

Example:

procedure TScriptForm.StartScript(sender: TObject); override;
begin
  CurrentTask := ETask(Self.TaskSelector.GetItemIndex());
  inherited;
end;
TScriptForm.Setup
procedure TScriptForm.Setup(caption: String = 'Script Form'; size: TPoint = [750, 500]; allowResize: Boolean = False);
Responsible for setting your TScriptForm up. This sets up the sekeleton of your TScriptForm ready to take in tabs.

TScriptForm.Show
procedure TScriptForm.Show();
Shows your TScriptForm after it has been setup. To run this you have to use Sync()

Example:

Sync(@MyForm.Show);
TScriptForm.Run
procedure TScriptForm.Run();
Basically a wrapper for TScriptForm.Show() so users don’t have to use Sync() directly. It is also a great method to override to setup your custom form things on like in the previous examples. If you do override it, you absolutely must use inherited on your override and it should be at the end of the method.