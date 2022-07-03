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
function ShowArea(e, el) {
  $("div",
    { e },
    [el]
  );
}

function StatusBar() {
  const [state, setState] = naiveState(0);
  const [click, disClick] = naiveEvent("click");
  
  // called $html returns reference of HTMLElement
  const div = $html("div",
    {
      class: "base"
    },
    $html("div",
      {
        class: "base"
      }
    )
  );

  disClick([
    () => {
      if (state > 5) {
        console.log("5 times");
      }

      console.log("clicked");
    }
  ]);


  return $("div",
    { click },
    [ShowArea(click, div)]
  );
}
```
