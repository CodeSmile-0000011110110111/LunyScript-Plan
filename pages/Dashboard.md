- Sprint1: {{query (and (todo now) [[sprint1]])}}
- [[BACKLOG]]
	- #+BEGIN_QUERY
	  { :title [:h3 "Backlog (Not Yet Assigned to a Sprint)"]
	    :query [:find (pull ?b [*])
	            :where
	            ;; 1. Find the Backlog page
	            [?p :block/name "backlog"]
	            ;; 2. Find blocks that reference that page
	            [?b :block/refs ?p]
	            ;; 3. Only look for tasks marked LATER
	            [?b :block/marker "LATER"]
	            ;; 4. EXCLUDE if the block has a 'sprint' property
	            (not [?b :block/properties ?props]
	                 [(get ?props :sprint)])
	    ]
	  }
	  #+END_QUERY
-