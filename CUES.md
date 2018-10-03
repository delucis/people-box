# Cues

The easiest way to edit cues is to use the built-in cue editor. Open the People Box in Max and click **Edit Cues** in the top-right corner. From here you can tweak existing cues or add and delete cues.

If you’re still interested in editing the cue files by hand, read on.

## Cue Syntax

Cues and other data used by the People Box are stored in `patchers/people-data.json`, which is written using the [JSON format][30af9ea1]. You can edit this file in Max, or use a text editor like TextEdit or [Atom](https://atom.io/).

  [30af9ea1]: https://www.digitalocean.com/community/tutorials/an-introduction-to-json "An Introduction to JSON | DigitalOcean"

Every cue has a number and can send one or more messages to the different sound file players: `player-1`, `player-2` and `player-3`.

You can send the following messages:

- ### `play`

  When sending a `play` message, it should be followed by the name of the sound file to play, e.g. `pb.19.wav`. (Make sure the sound file is in the `media` folder!)
  
  Optionally, a number can follow the file name to set the volume of the sound file in decibels, e.g. `-6.5`.
  
  #### Examples
  
  ```json
  {
    "cues" : {
      "19" : {
        "player-1" : "play pb.19.wav -6.5"
      }
    }
  }
  ```

- ### `stop`

  A `stop` message by default will stop the file playing more or less instantly (with a fade-out of 40ms).
  
  If a `stop` message is followed by a number, this is used as the fade-out time in milliseconds, e.g. `5000` will produce a fade-out of 5 seconds.

  #### Examples

  ```json
  {
    "cues" : {
      "70" : {
        "player-1" : "stop"
      },
      "120" : {
        "player-2" : "stop 5000"
      }
    }
  }
  ```

### Multiple messages per cue

Although the built-in cue editor in Max currently only allows you to add one command per cue, it is possible to have a cue trigger multiple messages. To do so you will need to manually edit the `patchers/people-data.json` file and add additional players to the cue, for example:

```json
{
  "cues" : {
    "1" : {
      "player-1" : "play pb.1.wav"
    }
,
    "2" : {
      "player-2" : "play pb.2.wav -3"
    }
,
    "3" : {
      "player-1" : "stop",
      "player-2" : "stop 5000"
    }
  }
}
``` 
