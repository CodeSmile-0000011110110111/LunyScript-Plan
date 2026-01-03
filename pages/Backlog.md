- DONE [[Diagnostics]] Profiling with ingame overlay (Unity) #luny
- DONE [[Diagnostics]] LunyScript Debug Hooks with ingame overlay (Unity) #lunyscript
- DONE [[Refactor LunyScript]] API #lunyscript
- DONE [[Lifecycle]] blocks with events (create/destroy, enable/disable) #lunyscript
- LATER [[Lifecycle]] register/create/enable API methods for regular code #lunyscript
	- Note: to fire LunyScript internal events eg Object.Destroy(x) => LunyObject.Destroy(x)
- ### Lifecycle concerns
	- NOW Manage framecount internally in LunyEngine
	  :LOGBOOK:
	  CLOCK: [2026-01-03 Sat 14:02:13]
	  CLOCK: [2026-01-03 Sat 14:02:15]
	  :END:
		- Unity: framecount is 0 in Awake & OnEnable, then increments to 1 before Start()
		- Godot: framecount is 0 throughout the first frame
	- NOW LunyEngine: observers should init right away (remove SceneService instance requirement)
	  :LOGBOOK:
	  CLOCK: [2026-01-02 Fri 21:28:33]
	  :END:
	- NOW OnReady handling => put objects in a queue and process the queue up front so that all new objects in this frame run OnReady before FixedStep or Update
	  :LOGBOOK:
	  CLOCK: [2026-01-02 Fri 23:43:45]
	  CLOCK: [2026-01-02 Fri 23:43:50]
	  :END:
	- LATER Move object registration & event handling down to Luny, since LunyObject provides the event hooks - those are useful for all frameworks!
	- LATER need to handle LunyObject parenting (including a disconnected hierarchy)
	- LATER Enabled state change should call OnEnable/OnDisable to child LunyObjects as well
	- LATER GetAllObjects() converts every object to a LunyObject wrapper! This should only do so for objects for which we have LunyScripts.
	- DONE LunyScriptRunner startup should register object with lifecycle manager which then runs the events
	  :LOGBOOK:
	  CLOCK: [2025-12-30 Tue 20:08:41]--[2025-12-31 Wed 12:11:03] =>  16:02:22
	  :END:
- LATER [[Event Handling Blocks]] foundation (eg Input, Collision, SendMessage, etc) #lunyscript
- LATER [[Diagnostics]] LunyScript Profiling Hooks for profiling individual scripts and runnables #lunyscript
- LATER [[Diagnostics]] Debug Blocks should not be filtered out in release builds (not executing)
- LATER [[LunyScript Hot Reload]] with manual triggers #lunyscript
- LATER [[Conditional Blocks]] (if/else) #lunyscript
- LATER [[Composite Blocks]] (loops, timers, coroutines) #lunyscript
- LATER [[Variable Blocks]] #lunyscript
- LATER [[Testing Infrastructure]] #luny #lunyscript
- LATER [[Resource Addressing]] (eg LunyUrl) #luny
- LATER [[Lua Integration]] #luny
- DONE Disable Editor-only blocks (create EDITOR define, return no-op block, skip null blocks)
- LATER Variables refactor to Vars.Global[] and maybe Vars.G[] as alias
-
-
- possible improvements
	- case insensitive activator object-script name matching
	- configurable name matching "starts with" or "contains"
	- add variable validation (log read access of non-existing variables instead of silently returning a default value)
	- local variables are bound to an object, but we should have metadata for debugging which global variables a script reads, and which ones it changes (or may change)