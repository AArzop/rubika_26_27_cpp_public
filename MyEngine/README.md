# MyEngine

The purpose of this project is to implement a tiny 2D engine using SFML to practice C++, to think about engine architecture, how to solve issues... from scratch. 

[Get back to main README](../README.md)

### Summary

1. [Threshold 0](#threshold-0)
2. [Threshold 1](#threshold-1)

### Resources

Here are useful links:
- [SFML doc](https://www.sfml-dev.org/documentation/3.0.2/)
- [ImGui](https://pthom.github.io/imgui_manual_online/)

## General notes

The implentation of this project is totally free. You can dd any method/member/... you want/need to solve issues. However, if you want to change the way the system works, please ask me first so that the entire class has the same architecture.

A `Logger.h` file has been added. It provides a (small) working log system. Logs might be life saving and absolutely useless at the same time. They provide the user/developer with information about the various systems. But to be useful, logs must be added during the development and provide useful/self-explaining information.

As you can see in `Profiler.h` (and used in `Main.cpp`), you can use macro to create markers that can be displayed in [PIX](https://devblogs.microsoft.com/pix/download/). This is a useful tool that can help you track costly processes... But such as Logs, it is simpler to add markers during the development (otherwise, the moment you will really need it, it will be empty). 

Try thinking about limit cases during all your development. By doing that, you will create a robust system and limit the number of bugs you will create.

## Threshold 0

The purpose of this threshold is to become familiar with the given code of the project. In its base version, the project compiles and works (even if it draws nothing). Three configurations are provided :
- Debug : `_USE_IMGUI` and `_USE_PROFILER` are defined. No optimization. This is the configuration you will work on 
- RelWithDebugInfo : `_USE_PROFILER` are defined.
- Release : `_USE_IMGUI` and `_USE_PROFILER` are not defined. Everything is optimized.

Take also a look at provided classes `DebugMgr` (which enables you to register a custom debug) and `Logger` (which enables you to log messages). Those two classes will be used alongside the development of the project.

## Threshold 1

As expressed previously, the purpose of this project is to create a very simple 2D engine that could run a simple game (Vampires Survivor, Binding of Isaac...) from a very naive perspective to a more complex one. To do so, various systems will be developped alongside this lesson : Entity Component System, texture manager, animation system, multi-threading, editors... depending on where we want to go.

Let's start very simple to familiarize yourself with the environment.

### Step 0

Our engines will be based on entities. Everything will derevied from the `Entity` class. It will be later composed of different components that will provide it with new behaviors but we will deal with that later. The header to implement the `Entity` class is provided. Add everything necessary to be able to instantiate it. A `TransformCompoment` member is part of the `Entity` class. This class is provided to avoid marix issues during the development. For now, it is a standlone class but this will change with the development of the ECS.

### Step 1

At this stage, multiple entities can be instantiate but they are not linked to anything. We need to group them into a `Scene`, so they get meaning. The header is provided to give you the different signatures of the method you must implement. However, you may need to modify it to match the following requirments:
- Store differents entities
- Methods to add/remove entities to/from the pull
- Entities must follow the life cycle of the `Scene`

### Step 2

Create now a new manager `SceneMgr` in the same way as I did for the `DebugMgr` for instance. Here is the list of what you must implement:
- Store multiple `Scene`.
- Store the information about which `Scene` is active (the active is the one currently played).
- A method to add a new scene. Two scenes cannot have the same name so you will need to handle that case for instance.
- A method to select the active scene based on its name. Be careful of the life cycle of the previous active scene if you change it.
- Life cycle methods

### Step 3

At this stage, everything should be in place... But you have now way to test it and now way to "see" if it is working. That is why we have a `DebugMgr`. Change your `SceneMgr` so it can draw its own debug window (**hint**: You might take a look at the `Logger` class). This debug must allow you to :
- See the various scene added to the manager
- Know which scene is currently active
- Inspect each scene to see its content (name, entity...)
- Buttons to switch scene, add entity...

**hint** : We are using ImGui to draw those debug.
