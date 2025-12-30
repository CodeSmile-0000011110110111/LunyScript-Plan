- DONE [[Diagnostics]] Profiling with ingame overlay (Unity) #luny
- DONE [[Diagnostics]] LunyScript Debug Hooks with ingame overlay (Unity) #lunyscript
- DONE [[Refactor LunyScript]] API #lunyscript
- LATER [[Lifecycle]] blocks with events (create/destroy, enable/disable) #lunyscript
- LATER [[Lifecycle]] create/enable engine API for regular code #lunyscript
	- Note: to fire LunyScript internal events eg Object.Destroy(x) => LunyObject.Destroy(x)
- LATER Lifecycle concerns
	- LATER Enabled state change should call OnEnable/OnDisable to child LunyObjects as well
	- NOW LunyScriptRunner startup should register object with lifecycle manager which then runs the events
	  :LOGBOOK:
	  CLOCK: [2025-12-30 Tue 20:08:41]
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