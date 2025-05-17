ProgressReport
This is what’s responsible for the in game screen report, often called as “paint” or HUDProgressReport in WaspLib.

You can easily toggle the usage this on or off by switching the variables:

WLSettings.RemoteInput.HUDReport

WLSettings.RemoteInput.Enabled

Note

Keep in mind that ProgressReport requires remote input.

type ProgressReport
Type responsible for handling the HUDProgressReport, also commonly called as “Paint” or InGame/OnScreen Progress Report.

ProgressReport.Terminate
procedure ProgressReport.Terminate();
Internal method called automatically on termination. This will do things such as free used assetsa and clear the progress report from the game screen.

ProgressReport.Setup()
procedure Self.Setup();
Internal method called when we need to setup TRSProgressReport.

ProgressReport.DrawBackground()
procedure TRSProgressReport.DrawBackground(fontColor: Int32);
Method that handles drawing the background of our Self. Usually called internally by Self.Update().

ProgressReport.DrawProgress()
procedure TRSProgressReport.DrawProgress(fontColor: Int32);
Method that handles drawing the text of our Self. Usually called internally by TRSProgressReport.Update().

ProgressReport.HideProgress()
procedure TRSProgressReport.HideProgress();
Used to hide Self. Usually called internally by TRSProgressReport.Update().

ProgressReport.Update
procedure TRSProgressReport.Update();
Main method that should be called to used to start and update ProgressReport.

To see Self.GetNextCycleColor() in action, which was just a fun experiment, uncomment:

//Self.TextColor := Self.GetNextCycleColor(Self.TextColor, 10);
var ProgressReport
Global ProgressReport variable.