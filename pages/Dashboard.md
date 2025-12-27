- Sprint1: {{query (and (todo now) [[sprint1]])}}
- [[BACKLOG]]
	- #+BEGIN_QUERY
	  { :title [:h2 "Backlog (No Sprints)"]
	    :query [:find (pull ?b [*])
	            :where
	            [?p :block/name "Backlog"]
	            [?b :block/refs ?p]
	            [?b :block/marker "LATER"]
	            (not 
	              [?b :block/refs ?t]
	              [?t :block/name ?tagname]
	              [(clojure.string/starts-with? ?tagname "sprint")]
	            )
	    ]
	  }
	  #+END_QUERY
-