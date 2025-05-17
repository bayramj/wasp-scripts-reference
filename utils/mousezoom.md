MouseZoom
Methods to handle the zoom levels with he mouse wheel.

This file was developed with help from data available through the RuneLite camera plugin.

type TRSMouseZoom
Record responsible to handle zooming with the mouse wheel and keep MM2MS.ZoomLevel in sync with the zoom slider.

RSMouseZoom.GetNext
function TRSMouseZoom.GetNext(value: Int32; down: Boolean): Int32;
function TRSMouseZoom.GetNext(value: Int32; amount: Int32 = 1; down: Boolean = True): Int32; overload;
Returns the next zoom level given your current one (value) and the direction you will be spinning the mouse wheel. You can optionally specify the number of scrolls you plan on doing via amount.

Example:

WriteLn('Current zoom value: ', value);
WriteLn('Next value on scroll up: ', RSMouseZoom.GetNext(value, False));
WriteLn('Next value on scroll down: ', RSMouseZoom.GetNext(value, True));
RSMouseZoom.Level2Slider
function TRSMouseZoom.Level2Slider(value: Int32 = -1): Int32;
As the name implies, this method is used to convert RSMouseZoom.ZoomLevel to MM2MS zoom slider levels (0..768 to 0..100).

Example:

WriteLn RSMouseZoom.Level2Slider(384); //should print 50.
RSMouseZoom.Slider2Level
function TRSMouseZoom.Slider2Level(value: Int32 = -1): Int32;
As the name implies, this method is used to convert MM2MS.ZoomLevel to RSMouseZoom.ZoomLevel levels (0..100 to 0..768). Unlike the previous method though, this one is not 100% accurate but good enough.

To understand why first you need to understand a few concepts:

Even though we use the range 0..100 for slider levels, it’s a made up range.

Because of this, the slider actually has only 96 positions and 4 dead levels: 13, 37, 63 and 87.

You can confirm this by trying to use Options.SetZoomLevel(13) or any other of those levels and then using Options.GetZoomLevel().

Each slider position actually has 8 RSmouseZoom zoom levels in it. TRSMouseZoom.MAX_ZOOM = 96*8 .

Having understood that, you can now understand why it is not 100% accurate. If each slider level has 8 rsmousezoom levels in it, it’s impossible to make it 100% accurate.

Example:

WriteLn RSMouseZoom.Slider2Level(50); //should print 384.
RSMouseZoom.Scroll
procedure TRSMouseZoom.Scroll(amount: Int32 = 1; down: Boolean; forceMove: Boolean = True);
procedure TRSMouseZoom.Scroll(amount: Int32 = 1; forceMove: Boolean = True); overload;
Performs a mouse scroll in the direction specified and updates RSMouseZoom.ZoomLevel and MM2MS.ZoomLevel accordingly. The scroll direction can be specified either with a boolean or with a positive/negative amount of scrolls, scroll up being positive. You can also otpionally tell it to move the mouse to the mainscreen before scrolling.

Example:

RSMouseZoom.Scroll(5, True);
RSMouseZoom.MaxZoom
procedure TRSMouseZoom.MaxZoom(down: Boolean = True);
Maxes the zoom limit in the direction you specified.

Example:

RSMouseZoom.MaxZoom(True); //will zoom out to the limit.
RSMouseZoom.MaxZoomBlind
procedure TRSMouseZoom.MaxZoomBlind(down: Boolean = True);
Maxes the zoom limit without knowing the current zoom level. This can be used to figure out the current zoom level if we don’t know it yes.

Example:

RSMouseZoom.MaxZoomBlind(True); //will zoom out to the limit.
RSMouseZoom.GetZoomLevel
function TRSMouseZoom.GetZoomLevel(): Int32;
This simply returns RSMouseZoom.ZoomLevel if it is already set, if it’s not set, it will attempt to set it up.

Example:

WriteLn RSMouseZoom.GetZoomLevel();
RSMouseZoom.SetZoomLevel
function TRSMouseZoom.SetZoomLevel(level: Int32): Boolean;
Set the specified zoom level. This assumes slider levels (so 0..100 range). This will often miss the target by a couple of zoom levels due to how zooming with the mouse wheel works. Assuming we end up within 4 zoom levels of the target level, it’s assumed successful.

Example:

RSMouseZoom.SetZoomLevel(75); //will attempt to zoom in/out until you are within 4 levels of 75.
RSMouseZoom.RunStressTest
procedure TRSMouseZoom.RunStressTest(iterations: Int32 = 19999);
A simple stress test of RSMouseZoom. This will zoom in/out continuously for whatever many times you specified and keep track of RSMouseZoom.ZoomLevel, MM2MS.ZoomLevel, and the fail rate of MM2MS.ZoomLevel and Options.GetZoomLevel() which should always be in sync.

Note

Be warned that you should never use this on an account you care! It can definitly get you banned!

Example:

RSMouseZoom.RunStressTest(39999); //will perform 40000 zoom in/outs randomly.
RSMouseZoom.DrawGraph
procedure TRSMouseZoom.DrawGraph();
Draw a simple graph of the RSMouseZoom data.

Example:

RSMouseZoom.DrawGraph();
var RSMouseZoom
Global RSMouseZoom variable.
