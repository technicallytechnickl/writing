---
title: NodePurple
layout: post
---

## NodeRed but Elixir

Define the "program" as a directed graph.  

GenServer1 ----msg--->GenServer2

All GenServers have standard :handle_call to handle the message as defind by the code put into the "Node".

GenServers naturally keep node context.  Flow supervisor can keep flow context (:ets?).  Overall Supervisor can keep global context.  Context accessible by all underlings.  

### Process
	Run the "development" application
	It points to a project directory structure
	While developing in the UI, the application generates actual code files as part of an application?, compiles, and loads them into that application
	Each "deployment" causes the application to be re-evaluated and changes applied.
	The project code is always running

### What the Development Application Does
	Look in directory -> Find map file -> Use map file to explore directory structure -> Generate folders and code if necessary or if existing code doesn't match map file.  As long as modules exist that are defined in the map, don't change existing code, other than the standard handle_call/handle_cast implementations. 
	Compile application and load into Beam with reference name.  (Need to point logs somewhere)

Does development application load the application with itself as a supervisor or does the application run independently? (I think it should be runnable independently, but the hooks to the UI won't work without running it via the development application)
How can the development application find and "connect" to a running project.  Needs to know where code is, needs access to "debug" and "context data". Maybe can't connect unless the project is started via the development application.

### Pages
	Each page can have multiple graphs that are unconnected though they can become connected.
	Each page has a supervisor that oversees the graphs on the page. 
	Each page has it's own description of how to render the page.  There can be a default with deltas based on user actions. If the delta file is lost, then the page can still be rendered in a default manner. 
	Each page has it's own graph file that contains the graph information. 


### Creating Connections
	Connecting two nodes creates a graph connection. Then the generator uses the graph to create pub-sub connections specific to the graph.  
	Connections are stored in a flat file.  When scanned if there is no connection, any pub/sub between the nodes is deleted, if it exists it is created. 
	This data structure should support other standards besides the "msg" type standard connection.  Can pass an alternative data structure and do other things with it. 
	Different color connections for different message types. 
	Use DOT notation:
	```
	digraph graphname {
    a -> b -> c;
    b -> d;
	}
	```
	Each edge can have it's own definition in the graph file.  -> Should only be by name.  Code defintion stored elsewhere. 


### Nodes
	Nodes have a display name and a generated unique ID.  UniqueIDs are used for the graph representation.
	Nodes can have other messages published and subscribed to just like any GenServer.  
	Nodes can also "do their own thing" independent of anything else happening, but have to respond to standard messages. 
	Nodes are genrated as GenServers when drawn.  

	Unique IDs have to comply with elixir module naming rules


### Installation
	Things like `mix deps.get` should be run automatically when needed by nodes.  
	Deploying hot reloads modules as necessary to add and remove pub-sub capabilities. 
	Deploying also writes to the graph description, creates node names, etc. 



### Required Data
	Graph structure
	Visualization data
		- Connection info from Graph structure
		- Color and shape information for each node
		- Location information for each node
		- Connector information (junctions?)
		- Order information for pages/tabs
	Code per node
	Code per page, code per project?

### Required Functionality
	UID Generator per node, per flow, per project
	Graph traversal and pub/sub checker
	Code generator
	Create graph file from drawing in UI

Location and drawing information keept in separate file from the code.  

Code stored as regular code and a definition of the directed graph.  


### Directory Structure
	Node Project
	├── 
	├── 
	├── Flows
	│   ├── Flow 1
	|	|	|-- flow1.map
	│   │   ├── Node1
	|	|	|	|-- Code Directory

All code used is stored in project (no need to download dependencies, but  need to update?)

Messages pass msg map. 

Can pass functions?

Deploying flows achieved by hot code reload so no state is lost unless desired?

Configurations end up being stored in the Node Code.  
Nodes can still reference environment variables if needed. 


Advanced: Directed graph connections can have definition of what kind of call is being made. 

Sources:
https://elixirforum.com/t/compiling-and-loading-modules-dynamically/32170/2

https://medium.com/@dinis.cruz/dot-language-graph-based-diagrams-c3baf4c0decc

Compiling and loading modules dynamically: https://elixirforum.com/t/compiling-and-loading-modules-dynamically/32170

Graph Description Language: https://en.wikipedia.org/wiki/DOT_(graph_description_language)

### Ports
https://renenyffenegger.ch/notes/tools/Graphviz/examples/index

