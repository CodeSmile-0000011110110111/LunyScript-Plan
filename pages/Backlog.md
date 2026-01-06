- DONE [[Diagnostics]] Profiling with ingame overlay (Unity) #luny
- DONE [[Diagnostics]] LunyScript Debug Hooks with ingame overlay (Unity) #lunyscript
- DONE [[Refactor LunyScript]] API #lunyscript
- ## Lifecycle concerns
	- DONE [[Lifecycle]] blocks with events (create/destroy, enable/disable) #lunyscript
	- DONE Manage framecount internally in LunyEngine
	  :LOGBOOK:
	  CLOCK: [2026-01-03 Sat 14:02:13]
	  CLOCK: [2026-01-03 Sat 14:02:15]--[2026-01-03 Sat 19:49:46] =>  05:47:31
	  :END:
		- Unity: framecount is 0 in Awake & OnEnable, then increments to 1 before Start()
		- Godot: framecount is 0 throughout the first frame
	- DONE LunyScriptRunner startup should register object with lifecycle manager which then runs the events
	  :LOGBOOK:
	  CLOCK: [2025-12-30 Tue 20:08:41]--[2025-12-31 Wed 12:11:03] =>  16:02:22
	  :END:
	- DONE LunyEngine: observers should init right away (remove SceneService instance requirement)
	  :LOGBOOK:
	  CLOCK: [2026-01-02 Fri 21:28:33]--[2026-01-03 Sat 20:06:02] =>  22:37:29
	  :END:
	- DONE OnReady handling => put objects in a queue and process the queue up front so that all new objects in this frame run OnReady before FixedStep or Update
	  :LOGBOOK:
	  CLOCK: [2026-01-02 Fri 23:43:45]
	  CLOCK: [2026-01-02 Fri 23:43:50]--[2026-01-03 Sat 22:50:19] =>  23:06:29
	  :END:
	- DONE Move object registration & event handling down to Luny, since LunyObject provides the event hooks - those are useful for all frameworks!
	- LATER [[Lifecycle]] register/create/enable API methods for regular code #lunyscript
		- Note: to fire LunyScript internal events eg Object.Destroy(x) => LunyObject.Destroy(x)
		- LATER create object via API and register it (should activate script if exists)
		- LATER get and destroy registered object via API
	- LATER update methods should not run when object is disabled in hierarchy (unregister handlers or check every frame?)
	- LATER need to handle LunyObject parenting (including a hierarchy with "gaps")
- ## LunyEngine Concerns
	- LATER
- ## LunyObject Concerns
	- DONE move _isEnabled and _isDestroyed (also: _nativeID, _name) to LunyObject base class
	  :LOGBOOK:
	  CLOCK: [2026-01-04 Sun 17:18:15]--[2026-01-04 Sun 17:18:18] =>  00:00:03
	  CLOCK: [2026-01-04 Sun 17:18:19]--[2026-01-04 Sun 20:46:08] =>  03:27:49
	  :END:
	- DONE rename with "Luny" prefixes everywhere
	  :LOGBOOK:
	  CLOCK: [2026-01-04 Sun 17:18:25]--[2026-01-04 Sun 18:04:57] =>  00:46:32
	  :END:
	- DONE rename As<> to Cast<>
	  :LOGBOOK:
	  CLOCK: [2026-01-04 Sun 17:18:27]--[2026-01-04 Sun 20:46:12] =>  03:27:45
	  :END:
- ## SceneService Concerns
	- LATER GetAllObjects() converts every object to a LunyObject wrapper! This should only do so for objects for which we have LunyScripts.
	- LATER GetSingleObject, convert to LunyObject if necessary, return proxy otherwise
	- LATER test scene (re-)load
- ## Failsafe Concerns
	- LATER return valid "error" objects
- ## Cleanup Concerns
- DONE prefix with Luny
- DONE refactor and remove LunyThrow
- ## Other Concerns
- LATER [[Event Handling Blocks]] foundation (eg Input, Collision, SendMessage, etc) #lunyscript
- LATER [[Diagnostics]] LunyScript Profiling Hooks for profiling individual scripts and runnables #lunyscript
- LATER Diagnostics add internal verbose logging with log levels (perhaps categories for filtering?)
- DONE [[Diagnostics]] Debug Blocks should be filtered out in release builds (not executing)
- LATER [[LunyScript Hot Reload]] with manual triggers #lunyscript
- LATER [[Conditional Blocks]] (if/else) #lunyscript
- LATER [[Composite Blocks]] (loops, timers, coroutines) #lunyscript
- LATER [[Variable Blocks]] #lunyscript
- LATER [[Testing Infrastructure]] #luny #lunyscript
- LATER [[Resource Addressing]] (eg LunyUrl) #luny
- LATER [[Lua Integration]] #luny
- DONE Disable Editor-only blocks (create EDITOR define, return no-op block, skip null blocks)
- LATER Variables refactor to Vars.Global[] and maybe Vars.G[] as alias
- ## Testing Concerns
- LATER smoke test scene check should be improved, remove hardcoded strings
-
-
- possible improvements
	- case insensitive activator object-script name matching
	- configurable name matching "starts with" or "contains"
	- add variable validation (log read access of non-existing variables instead of silently returning a default value)
	- local variables are bound to an object, but we should have metadata for debugging which global variables a script reads, and which ones it changes (or may change)