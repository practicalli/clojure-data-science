## Run Notespace on REPL startup
[Example Notespace project](https://github.com/practicalli/scicloj-notespace-simple-demo) is a project with simple examples and also launches an empty notespace webpage on REPL startup.

{% tabs deps="Clojure CLI tools", lein="Leiningnen" %}

{% content "deps" %}
Use a deps.edn file that includes the `scicloj/notespace` library


## Creating a new project
Use Clojure CLI tools ([:project/new](http://practicalli.github.io/clojure/clojure-tools/projects/create.html)) to create a project.

```
clojure -X:project/new :template app :name practicalli/notespace-demo
```

Edit the `deps.edn` file

Add `scicloj/notespace` library as dependency

Use [practicalli/clojure-deps-edn](http://practicalli.github.io/clojure/clojure-tools/install/community-tools.html) user configuration or add an `:env/dev` and `:inspect/portal-clj` aliases to the project `deps.edn` file

```
{:paths ["src" "resources"]
 :deps
 {org.clojure/clojure {:mvn/version "1.10.1"}
  scicloj/notespace   {:mvn/version "3-alpha3-SNAPSHOT"}}
 :aliases
 {:env/dev {:extra-paths ["dev"]}
  :inspect/portal-cli {:extra-deps {djblue/portal {:mvn/version "0.6.4"}}}}}
```


{% content "lein" %}
## Creating a new project
Use Leinigen to create a new project

```
lein new app practicalli/notespace-demo
```

Edit the project.clj file

Add notespace as a dependency to the project configuration

add a `:dev` profile with `:resource-paths` which adds the `dev` directory to class path.  Leiningen uses the `:dev` profile unless another profile is specified.

```
(defproject practicalli/notespace-demo "0.1.0-SNAPSHOT"
  :description "Notespace journal - simple demo"
  :url "https://practicalli.github.io/data-science/notebooks/notespace/"
  :license {:name "Creative Commons Attribution Share-Alike 4.0 International"
            :url  "https://creativecommons.org"}
  :dependencies [[org.clojure/clojure "1.10.1"]
                 [scicloj/notespace "3-alpha3"]]
  :main ^:skip-aot practicalli.notespace-demo
  :target-path "target/%s"
  :profiles {:dev     {:resource-paths ["dev"]
                       :dependencies   [[djblue/portal "0.6.4"]]}
             :uberjar {:aot :all}})
```

{% endtabs %}


## Add namespace to start notespace with REPL
Create a `dev/user.clj` source code file

Add a `user` namespace definition that requires notespace and portal

Add a call to start notespace

Add a call to start Portal and connect it to the REPL as a tap> source

Add notespace and portal helper functions

```
(ns user
  (:require [notespace.api :as notespace]
            [portal.api :as inspect]))

;; Start Notespace
(notespace/init-with-browser)

;; Start Portal
;; Open a portal inspector window using default nord theme
(inspect/open {:portal.colors/theme :portal.colors/solarized-light})

;; Add portal as a tap> target
(inspect/tap)


(comment

  ;; Notespace helpers
  ;;;;;;;;;;;;;;;;;;;;;;

  ;; Initialise notespace, headless or open browser
  (notespace/init)
  (notespace/init-with-browser)


  ;; Portal helpers
  ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

  ;; Open Portal window with nord theme (default)
  (inspect/open)

  ;; Open Portal window with solarized-dark theme
  (inspect/open {:portal.colors/theme :portal.colors/solarized-dark})

  ;; Open Portal window with solarized-light theme
  (inspect/open {:portal.colors/theme :portal.colors/solarized-light})

  ;; Clear all values in the portal inspector window
  (inspect/clear)

  ;; Close the portal window
  (inspect/close)

  ) ;; End of rich comment block

```





## Run a REPL for the project

{% tabs depsstart="Clojure CLI tools", leinstart="Leiningnen" %}

{% content "depsstart" %}
Open a terminal and run a REPL using the `:env/dev` and `:inspect/portal-cli` aliases

```
clojure -M:env/dev:inspect/portal-cli
```


{% content "leinstart" %}
Open a terminal and start a REPL with Leinigen, using the `:dev` profile by default

```
lein repl

```


{% endtabs %}
