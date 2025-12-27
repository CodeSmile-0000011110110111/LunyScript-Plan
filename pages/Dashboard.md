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
- #+BEGIN_QUERY
  { :title [:h2 "Backlog (Unassigned)"]
    :query [:find (pull ?b [*])
            :where
            [?p :block/name "backlog"]
            [?b :block/page ?p]
            [?b :block/marker "LATER"]
            ;; Filter: Exclude if 'sprint' exists in properties
            (not-join [?b]
              [?b :block/properties ?props]
              [(get ?props :sprint)])
            ;; Filter: Exclude if a child bullet has 'sprint'
            (not-join [?b]
              [?child :block/parent ?b]
              [?child :block/properties ?cprops]
              [(get ?cprops :sprint)])
    ]
  }
  #+END_QUERY
-
- #+BEGIN_QUERY
  { :title [:h2 "Current Sprint Items"]
    :query [:find (pull ?b [*])
            :where
            [?b :block/marker "LATER"]
            [?b :block/properties ?props]
            [(get ?props :sprint) ?v]
            ;; Convert the value to a string to be safe
            [(str ?v) ?str-v]
            ;; Use a string match for "1"
            [(= ?str-v "1")]
    ]
  }
  #+END_QUERY