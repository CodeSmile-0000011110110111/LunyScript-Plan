- REFACTOR ScenePreprocessor currently loads scripts for existing objects. We should re-design this to always instantiate scripts even without context. For one, they might "instantiate themselves" via OnStartup event blocks ie OnStartup(Prefab.Spawn(nameof(TheScript))) If not that, then something else might spawn the corresponding object.
-
- **Hot reload is per-ScriptType:**
  1. Detect script type changed (manual API trigger for now, file watcher later)
  2. Find all RunContexts with matching ScriptType
  3. For each context:
	- Preserve: Object, Variables, InspectorVariables
	- Clear: UpdateRunnables, FixedStepRunnables, LateUpdateRunnables
	- Create new script instance
	- Call script.Initialize(context) with SAME context
	- Call script.Build() - repopulates runnables
	  4. GlobalVariables unchanged (shared reference)
	  5. Ask user about LunyScript callbacks for unload and reload - enabling users to make scripted hot reload changes (ie reset variables on hot reload). These should be blocks in the Build() method: OnBeforeReload(Log("unloading ..")), OnAfterReload(Log("loading .."))
	- decision: OnBeforeReload() runs from within the existing runnable (modify variables before new instance's OnStartup runs)
	- decision: OnAfterReload() runs after OnStartup() on the new instance
	- decide: should hot reloading scripts run their OnStartup() and OnShutdown() runnables or not?
	  
	  **No state preservation attributes** - entire context recreated, all blocks replaced. Assume full invalidation.
-