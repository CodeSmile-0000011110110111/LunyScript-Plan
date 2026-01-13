## Lifecycle
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
	-
- ## Diagnostics
	- DONE [[Diagnostics]] Profiling with ingame overlay (Unity) #luny
	- DONE [[Diagnostics]] LunyScript Debug Hooks with ingame overlay (Unity) #lunyscript