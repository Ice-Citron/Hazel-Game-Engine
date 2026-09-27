# Hazel — C++ Game Engine

An attempt to build a C++17 3D game engine through The Cherno's Hazel
series. The code contains the application foundation:

- A GLFW window and input controls.
- Templated event dispatch.
- Layers and overlays.
- OpenGL shaders.
- Dear ImGui integration.

## Why I started this project

My friends and I originally intended this as our IB CAS project.
Initially, we wanted to build our own C++ game engine, then use this same 
engine to create our own Minecraft-style game. Ultimately, this scope was too
 ambitious, and we did not complete the engine nor the game. Development stopped 
 when I shifted my attention to AI and my GPT-2 reproduction extended essay.

In hindsight, that was the right decision for me. Given that currently graphics
programming is no longer the frontier, and frontier AI is more relevant than 
ever.

## What the code contains

- **Application core.** An application loop connects the window to the
  layer stack. Each layer has update, event, and interface hooks.
- **Window and input.** GLFW creates the window and processes input.
  The code also provides direct keyboard and mouse state queries.
- **Event dispatch.** A templated dispatcher selects handlers by event
  type. Category flags group related events.
- **Layers and overlays.** Overlays receive events before ordinary
  layers. An event stops when a layer marks it as handled.
- **OpenGL foundation.** The application contains an indexed triangle
  example with vertex and index buffers.
- **Shader class.** The code compiles vertex and fragment shaders.
  It links the program and reports compiler or linker errors.
- **Dear ImGui integration.** The interface enables docking and
  multiple platform windows through the GLFW and OpenGL backends.
- **Diagnostics.** Engine and client logs use spdlog. Debug assertions
  check conditions during development.

The Sandbox example checks the Tab key through two paths: direct state
queries and key events. It also defines a small Dear ImGui test window.

## Read the code

Start with [SandboxApp.cpp][sandbox] to see how an application uses Hazel.

Then read [Application.cpp][application] for the main loop and event flow.
[Event.h][events] defines the dispatcher. [LayerStack.cpp][layers] controls
the order of layers and overlays.

## Repository structure

```text
Hazel/
├── src/
│   ├── Hazel/           # Application, events, layers, shaders, and UI
│   ├── Platform/        # Windows and OpenGL implementations
│   └── Hazel.h          # Public include for client applications
└── vendor/              # Third-party dependencies
Sandbox/
└── src/SandboxApp.cpp   # Example application
GenerateProjects.bat     # Original project-generation script
Hazel.sln                # Visual Studio solution
premake5.lua              # Build configuration
LICENSE                  # Repository licence
```

## Build configuration

The original build targets Windows x64 with C++17 and Visual Studio 2022.
It defines Debug, Release, and Dist configurations. Hazel builds as a
static library. Sandbox builds as a separate executable.

The project uses Git submodules for GLFW, Dear ImGui, GLM, and spdlog.
Initialise these dependencies from the repository root:

```bash
git submodule update --init --recursive
```

`GenerateProjects.bat` expects `vendor/bin/premake5.exe`.
The repository does not include that executable. With Premake 5 on your
command path, use `premake5 vs2022` to regenerate the solution.

Open `Hazel.sln` and select `Sandbox` as the startup project.
These setup instructions still need verification on a fresh Windows system.

## Credits and licence

The architecture follows [The Cherno's Hazel series][hazel].
This repository records my work through the tutorial.

The root [LICENSE](LICENSE) contains the Apache License 2.0.
Third-party dependencies retain their own licences.

[opengl]: https://github.com/Ice-Citron/OpenGL-Series
[hazel]: https://github.com/TheCherno/Hazel
[sandbox]: Sandbox/src/SandboxApp.cpp
[application]: Hazel/src/Hazel/Application.cpp
[events]: Hazel/src/Hazel/Events/Event.h
[layers]: Hazel/src/Hazel/LayerStack.cpp
