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

<details>
 <summary><h2>processor</h2></summary>
</details>

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
