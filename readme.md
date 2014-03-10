# QML PollKey

A simple way of supporting polling of keyboard keys with qml.

## Motivation

There's no built-in way in qml to check whether a key is held down or not. There's only the onPressed and onReleased events. This makes it difficult to implement some features, such as smoothly moving and object when a key is held down.

## How it works

It's really simple, the entire source code is only 15 lines.

It just keeps a map of all the keys and whether they were last pressed or released. The onPressed and onReleased events are used to update the map.

## Example usage

Just add a KeyMap where you want to be able to poll keys.

    Rectangle {
        KeyMap{ //this objects keeps track of the key
            id: keyMap
        }
        //the keymap still need key events to update the map, so let's forward them
        Keys.forwardTo(keyMap);
        
        //lets test that it actually works
        Timer {
            running: true; repeat: true
            interval: 200
            onTriggered: {
                console.log("Left key is held down:", keyMap.isKeyDown(Qt.Key_Left));
            }
        }
    }

If you set it up in this way, the map will also respect the keyboard focus rules of qml.
