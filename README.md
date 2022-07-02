## render queue

```
+-------+
|+------|-------+
||  |  || |  |  |
|+------|-------+
+-------+

 SOPT Limited
 
 
Children shouldn't update rendering before parent
```

## render

```
           +--------+
           | Layout |
           +--------+
               |
         +--------------+
         | singleLayout |
         +--------------+
         /             \
 +-----------+      +------------+
 | Container |      | MappingDOM |
 +-----------+      +------------+
                          |
                     +----------+
                     | HTML DOM |
                     +----------+
```

## reactive

```
         +------------+
         | Dispatcher |
         +------------+
          /          \
+-----------+      +------------+    +----------+
| Container |      | MappingDOM | -- | HTML DOM |
+-----------+      +------------+    +----------+
          \          //
       +---------------+
       | mappingLayout |
       +---------------+
```

## default enabled memoization

```
when properties.parameters has changed,
should re-exec calling the dispatcher.
```

## enabled SOPT for render queue with validity descriptor

```
   [ ]                            0
    |
   [ ]                           0,0
   / \
 [ ] [ ]                     0,0,0 | 0,0,1
      |
     [ ]                               0,0,1,0
    / | \
  [ ][ ][ ]          0,0,1,0,0 | 0,0,1,0,1 | 0,0,1,0,2
   |    / \
  [ ] [ ] [ ]    0,0,1,0,0,0 |      0,0,1,0,2,0 | 0,0,1,0,2,1
```

## Example
```js
function ShowArea(el) {
  return $(
    "div",
    {
      "click": [
        (e) => { el.style.visibility="hidden"; }
      ]
    }
  )
}

function StatusBar() {
  const contentArea = document.createElement("div");

  return $(
    "div",
    [contentArea, $(ShowArea, contentArea)]
  );
}
```
