# How to use applescript to balance the airpod output at MacOS

## Create a script: `keepVoiceBalance.applescript`
```applescript
tell application "System Preferences"
	quit
	delay 1
end tell

tell application "System Preferences"
	activate
	reveal anchor "output" of pane id "com.apple.preference.sound"
	delay 1 -- If you get an error, it's possible this delay isn't long enough.
end tell

tell application "System Events"
	tell slider 1 of group 1 of tab group 1 of window 1 of process "System Preferences"
		set value to 0.5
	end tell
end tell
```

## Run it
Now double click it.

And hit the `run`

## The potiential reason of why airpod got wrong volume balance
I don't know, but by letting the `Loopback` open, things working good without problems.