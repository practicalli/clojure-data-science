# Webscraping with Enlive

quickly selecting elements based on CSS and/or Xpath

https://clojureverse.org/t/best-library-for-querying-html/1103

```clojure
(require '[net.cgrand.enlive-html :as enlive])

(let [doc (enlive/html-snippet "<div class='hello'>Hello, <em>world<em></div>")
      em  (enlive/select doc [:.hello :em])]
  (enlive/texts em))
```

## Including Enlive

## Searching for tags
