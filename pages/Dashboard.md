- #+BEGIN_QUERY
  { :title [:h2 "Sprint 1 (Child Property Version)"]
    :query [:find (pull ?parent [*])
            :where
            ;; 1. Find the child block that has the property
            [?child :block/properties ?props]
            [(get ?props :sprint) ?v]
            [(str ?v) ?str-v]
            [(= ?str-v "1")]
            
            ;; 2. Find the parent of that child
            [?child :block/parent ?parent]
            
            ;; 3. Ensure the parent is a task marked LATER
            [?parent :block/marker "LATER"]
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
- new item
- kuk