# PursuedPyBear

PursuedPyBear, also known as `ppb`, exists to be an educational
resource. Most obviously used to teach computer science, it can be a
useful tool for any topic that a simulation can be helpful.

## A Game Engine

At it's core, `ppb` provides a number of features that make it perfect
for video games. The `GameEngine` itself provides a pluggable subsystem
architecture where adding new features is as simple as subclassing and
extending `System`. Additionally, it contains a state stack of `Scenes`
simple containers that let you organize game scenes and UI screens in a
simple way.

The entire system uses an event system which is as extensible as the
rest of the system. Register new values to existing event types, and
even overwrite the defaults. Adding a new event system is as simple as
calling `Engine.signal` with a new datatype. Instead of a publisher
system the engine knows everything in its own scope and only calls
objects with appropriate callbacks. The most basic event is `Update`
and your handlers should match the signature
`on_update(self, update_event, signal)`.

## Guiding Principles

Because `ppb` started to be a game framework great for learning with,
the project has a few longterm goals:

### Education Friendly

Non-technical educators should feel comfortable after very little
training. While some programming knowledge is required, the ability to
think in objects and responses to events allows educators to only focus
on their lessons.

### Idiomatic Python

A project built on `ppb` should look like idiomatic Python. It also
should look like modern Python. As such, we often add new language
features as soon as they're available, letting a new user always know
ppb runs on the latest Python.

### Object Oriented and Event Driven

`ppb` games are built out of instances of objects that inherit from
`EventMixin`. Each object only has enough information to respond to the
event provided, which always includes the current `BaseScene`. Because
`ppb` doesn't have a master list of events, you can provide new ones
simply to add more granular control over your game.

### Hardware Library Agnostic

Because `ppb` strongly tries to be extensible and pluggable, each
hardware extension can provide its own hooks to `ppb`, and you can
nearly seamlessly switch between various Python libraries.

## Try it

Install ppb in the standard method:

```bash
pip install ppb
```


`ppb` provides a `run` function that makes it simple to start single
screen games.

To make a very simple game, make a directory and add an image file
called `ship.png` to it. Then add the following to a python file and
run it.

```python
import ppb


class Ship(ppb.BaseSprite):

    def on_update(self, update_event, signal):
        self.position += 0, -(4 * update_event.time_delta)


def setup(scene):
    scene.add(Ship(pos=(0, 3.5)))


ppb.run(scene_kwargs={"set_up": setup})
```

## Compatibility

`ppb` is guaranteed compatible with Python 3.7. The event system uses
dataclasses so you might need to inject a shim into your environment if
you use earlier versions. That said, it is strongly encouraged you use
3.7 to develop `ppb` projects.

## Get Involved

The fastest way to get involved is to check out the [ongoing
discussions.](https://github.com/ppb/pursuedpybear/issues?q=is%3Aissue+is%3Aopen+label%3Adiscussion)
If you're already using `ppb` feel free to report bugs, suggest
enhancements, or ask for new features.

If you want to contribute code, definitely read the relavant portions
of Contributing.MD
