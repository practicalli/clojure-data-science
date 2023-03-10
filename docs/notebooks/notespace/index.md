# Notespace - data science journal
[Notespace](https://github.com/scicloj/notespace) generates a data science journal from a Clojure namespace, to give a simple to use literate programming experience.

The [notespace introduction](https://scicloj.github.io/notespace/doc/notespace/v3-experiment1-test/index.html) shows how to create a Clojure namespace into a notespace.  Clojure values, generative functions, markdown and graphics are defined using `notespace.kinds` as meta-data on Clojure expressions in the namespace.

Run notespace listening to all changes, or just show a particular view (useful for large notespace) or even just update a line.


## Example project with notespace
Use the [example Notespace project](https://github.com/practicalli/scicloj-notespace-simple-demo) which contains simple examples and also launches an empty notespace webpage and Portal data inspector window on REPL startup.

Start a REPL for the project with Leiningen or Clojure CLI tools (version 1.10.1.697 or greater and aliases from [practicalli/clojure-deps-edn](https://github.com/practicalli/clojure-deps-edn))

```
lein repl

clojure -M:env/dev:inspect/portal
```

Wait a few seconds for the Portal and Notespace pages to load into your browser.

Evaluate the `(notespace/listen)` expression and the current namespace is loaded into the Notespace page.  If the Notespace page stops updating, evaluate this expression again.

Wrap values and function calls with the `tap>` function to see the values in the Portal window.


> #### Hint::Emacs support - Clojure CLI tools
> the [example Notespace project](https://github.com/practicalli/scicloj-notespace-simple-demo) contains a `.dir-locals.el` file for Clojure CLI tools, using the `:env/dev` and `:inspect/portal-cli` aliases from [practicalli/clojure-deps-edn](https://github.com/practicalli/clojure-deps-edn) user level configuration.
>
> When running `cider-jack-in` the aliases are automatically added to jack-in startup command.
