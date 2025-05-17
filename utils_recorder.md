Recorder
Heavily based in Olly’s SimbaRecorder: https://github.com/ollydev/SimbaRecorder

This was modified to:

Allow recording while using remoteinput

Add frame filters to hide Username/XPBar.

Things to keep in mind when using recorder:

It spawns another simba thread, which means it will count towards the WaspLib maximum thread limit.

This can be used to record the last few seconds of a script shutting down/crashing.

type Recorder
type Recorder = record(TSRLBaseRecord) class var
PID: Integer;
Debugging: Boolean;
end;
Recorder.Start
procedure Recorder.Start(window: PtrUInt; seconds: Int32; directory: String; userBox, expBox: TBox); static; overload;
procedure Recorder.Start(seconds: Integer; directory: String; userBox, expBox: TBox = []); static; overload;
Start the recorder.

window should be the window you want to record, hidding this parameter will use SimbaTargetWindow() for it.

seconds is the amount of “last” seconds you want the recorder to record.

directory is the directory you want the file to be saved to.

userBox and expBox are “box filters” to hide username and XPBar.