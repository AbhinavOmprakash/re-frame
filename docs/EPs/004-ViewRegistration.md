## EP 003 - View Registration

> Status: Placeholder. Don't read yet. 


### Abstract 

Broadbrush:
   - views registered via a new `def-view` function
   - like other re-frame registration functions, `def-view` associates a `keyword` with a (reagent) render function
   - the registered view keyword (eg: `:my-view`) can be used in hiccup to identify the renderer. eg:  `[:my-view  "Hello world"]`
   - `def-view` allows various values to be `injected` as args into the view render
   
What might need to be injected (as args) into a view:  

  - `subscribe` and `dispatch` 
  - a `frame` supplied via `context`  (subscribe and dispatch from frame)
  - other context: data from higher in the DOM tree
  - annimation?  CSS  ?

XXX searches up the DOM heirarchy looking for a `frame` context then extracts dispatch and subscribe.  Sounds inefficient. 

### Code Doodles

Associate the keyword `:my-view-id ` with a renderer using `def-view`:
```clj
(def-view 
   :my-view-id 
   
   ;; injection function
   ;; indicate what subscriptions we wish to obtain 
   ;; obtain a dispatch for use 
   ;; get the context id if you want to 
   ;; 
   :subscriptions 
   (fn [_ id]
      {:subs [[:item ]] 
       :context ["name1", "name2")})

       
   ;; the renderer
   ;; last argument `ins` is a map of:
   ;;    - `:subs` - a vector of subscription values? 
   ;;    - :dispatch and :subscribe 
   ;;    - :context - a vector of context values
   ;; 
   (fn [a-str  ins]
     (let [XXXX] 
       )))
```

Use of `:my-view-id `:
```clj
[:my-view-id  "Hello"] 
```


Misc Notes:
   
   - reagent hiccup will be changed/monkey-patched so that views can be identified by keyword
   - Views are the leaves of the signal graph. They need to subscribe and dispatch. 
   