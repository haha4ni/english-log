- 填上日期就會在下方出現
- TODO 哈摟
  SCHEDULED: <2099-10-31 Mon>
-
-
- #+BEGIN_QUERY
  {:title "next week deadline or schedule"
      :query [:find (pull ?block [*])
              :in $ ?start ?next
              :where
              (or
                [?block :block/scheduled ?d]
                [?block :block/deadline ?d])
              [(> ?d ?start)]
              [(< ?d ?next)]]
      :inputs [:today :28d-after]
      :collapsed? false}
  #+END_QUERY
-
- #+BEGIN_QUERY
  {:title " Scheduled TODOs"
  :query [:find (pull ?b [*])
  :where
  [?b :block/scheduled ?d]
  [?b :block/marker ?marker]
  [(not= ?d nil)]
  [(contains? #{"" "NOW" "LATER" "DOING" "TODO"} ?marker)]]
  :collapsed? false}
  #+END_QUERY
-