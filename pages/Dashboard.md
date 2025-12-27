## Current Sprint
- #+BEGIN_QUERY
  { :title [:h3 "Active Items: Sprint 1"]
    :query [:find (pull ?b [*])
            :where
            [?b :block/marker "LATER"]
            [?b :block/properties ?props]
            [(get ?props :sprint) ?s]
            [(= ?s 1)]
    ]
  }
  #+END_QUERY
- ---
- ## [[BACKLOG]]
	- #+BEGIN_QUERY
	  { :title [:h3 "Backlog (Not Yet Assigned to a Sprint)"]
	    :query [:find (pull ?b [*])
	            :where
	            ;; 1. Find the Backlog page
	            [?p :block/name "Backlog"]
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
- {{query (property sprint)}}
-
-