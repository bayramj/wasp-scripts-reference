RSClient
Extensions to TRSClient.

One thing to keep in mind is that WaspLib enforces the use of Remote Input by default.

To disable it you have to use either of this snippets in your scripts:

{$DEFINE SRL_DISABLE_REMOTEINPUT}
//or
begin
WLSettings.RemoteInput.Enabled := False;
end;