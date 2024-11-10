---
title: Scenic_Overview
layout: post
---


Scenic is a library in Elixir for creating GUIs.  Scenic is primarily targeted at IoT type devices, but can be used for any portable application.  The stated goals are:
1. **Small, fast, simple.**  Scenic is targeting 20-30MB including Linux, Erlang, and Scenic.
2. **Robust.**  This is provided largely by the Erlang VM and OTP. 
3. **Remotable.** Managed remotely in the field.
4. **Approachable.** Not web development, but easy to develop an interesting UI.
5. **Secure.**  Simple, no open ports, static asset hashing.
6. **Know where the brain is.**  The brain remains on the device.
7. **Software is Portable on New Hardware.** Again, provided by the Erlang VM

The Scenic documentation seems incomplete.  This seems to stem from Scenic still being in early development and major changes happening with each release.  Therefore, jumping into it with any how-to blogs and such results in much confusion. One example for me was push_graph.  In the first example I found, it was explicitly used.  Then I found documentation that said not to use it, and to instead use it as a return opt.  Then I read the v0.11 release notes saying it is back and to use it. 

Scenic is a three layer system:
1. **Scene Layer** - Like a web page.  Graph is heirarchical layer of things that can be drawn. Can apply styles and transforms.
2. **ViewPort Layer** - Sits between the Scene and the Drivers. Takes data from Scene to Driver and vice versa.
3. **Driver Layer** - Knows about the hardware, but know nothing about the Scene layer. Also collect user input.

### Scene
Like a webpage. Is a GenServer. Defines the Graph, handles events, and are reusable as Components.

### ViewPort
Intermediate management layer.  One ViewPort per window/session.  Normalizes Graph on the way to driver, routes user input up from the driver.

### Driver
Specific to hardware. Can mix and match for different purposes. 


### The Service
Hosted service for Scenic applications. User Auth, UI remoting, audit trails, proxy services. www.kry10.com


Graph can be built at compile time or run time.  Think about when you can get away with doing something.  Doing at compile time speeds up boot to first screen. (@graph). 

push_graph gets added to scene, and tells ViewPort that graph is ready to be displayed. 

A button is a scene and is a separate GenServer. 

There's a built in navbar component.  Includes a dropdown 

Can pass a set of new colors for components. 

Layouts are built using matrices. Different from HTML because you know the device screen size. 

## Creating Defender

In config.exs, change ```size``` to the desired screen size. 

Start the app with ```mix scenic.run```. 

Define the ship with a size, radius, etc. 

If using rounded_rectangle/3, the ```translate``` opt will move the object in (x, y) to the desired location. 

Is ```request_input``` necessary? It doesn't sound like it for a default single scene, only when there are  scenes that need to capture the input. 

Have to draw new object locations on a fresh graph.