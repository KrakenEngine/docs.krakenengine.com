---
title:  "Source Branches, Hydra Math Library, Asynchronous API"
published: true
permalink: 2018-07-29-kraken-update
summary: "Build system update, new source branches, Asynchronous API design"
tags: [news]
---

## Build System Update

The dust is starting to settle after setting up CMake to build the Kraken runtime library.  I've integrated continuous integration, using VisualStudio Online for Windows and Travis CI for other platforms.  Once the project is a bit further along, I will likely spin up bespoke CI and test infrastructure so that I can get controlled performance regression checking tests integrated.  It is essential to enable anyone to replicate the Kraken runtime builds on their own; however, I also indend to distribute pre-built binaries for anyone that prefers.

## Hello, Hydra

The Kraken math library has been broken out into a separate project, [Hydra](https://github.com/KrakenEngine/hydra).  The CMake scripts statically link this in Kraken runtime builds; however, it can now be used indepedently as well.  As part of this refactoring, I have changed all Hydra datatypes to POD data types.  This means we can't have constructors and destructors, so I have implemented "Create" static methods for all of these types.  The advantage of POD is that they can easily be accessed from array structures mapped from storage, network, or to the GPU.  This will also enable more convenient use of SIMD operations affecting multiple instances of these objects.

## Source Branches

I have simplified the branches to track the main areas of work:

* **feature-metal** for implementation of a modernized Metal-based iOS and macOS back-end.
* **feature-vulkan** for implementation of a modernized Vulkan-based Windows, Linux, and Android back-end.
* **feature-gltf** for implementation of [Khronos GLTF](https://www.khronos.org/gltf/) scene format support.

The Metal and Vulkan back-ends will require new shaders and significant changes to the rendering pipeline.  As the existing code is updated, I will be replacing it with a purely PBR based lighting model.

## Asynchronous API Design

I have been giving a lot of thought into API Design recently, as Kraken grows into a more disciplined, stable, and documented interface.  A design-goal of this interface is be to express the asynchronous nature of Kraken's rendering and audio threads explicitly.  Scene graph changes will be asynchronous -- the primary interaction with Kraken's runtime will be the submission of an asynchronously executed, transactional command buffer.  The transactions themselves will be simple POD types composed of Hydra primitives.  They will be easily reused, composed on multiple threads, and require no heap memory allocations.

If the calling thread blocks or does not submit new commands for a frame, Kraken must have a defined behavior and continue operating in a reasonable manner.  This should reduce the reliance of VR runtime fallbacks, such as synthesis of frames through reprojection.
