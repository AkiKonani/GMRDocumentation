# Improving the mesh net

Sometimes there seems to be disconnects between mesh polygons.
This seems usually the case when the pathfinding system seems to fail to find a path.

## How to fix polygon disconnects

### Visualizing the mesh net

This can be done with the [Movement](https://github.com/AkiKonani/GMRAddOns/tree/main/AddOns/Movement) add-on. Please see [installation instructions](https://github.com/AkiKonani/GMRAddOns#gmr-addons).

```
/script toggleMeshVisualization()
```

(a macro with this command can also be created and bound to a key ;-))

### Identifying disconnects

![](images/improving-the-mesh/WoWScrnShot_111822_164222.jpg)

The mesh polygons are visualized with green lines.

Polygons that are connected with the polygon, that the character stands in, are shown.

A neighboring polygon which seems disconnected from the polygon from the previous image:

![](images/improving-the-mesh/WoWScrnShot_111822_164829.jpg)

After the polygons have been connected:

![Step 5](images/improving-the-mesh/WoWScrnShot_111822_165855.jpg)

### Connecting polygons

Given two polygons to connect.

1. Move the character to a position inside the first polygon.
2. Run `/script setFirstOffMeshConnectionPoint()`
3. Move the character to a position inside the second polygon.
4. Run `/script setSecondOffMeshConnectionPoint()`
5. Save the connection. There are two options available:
   * For bidirectional connections: `/script saveOffMeshConnection(true)`
   * For one-way connections: `/script saveOffMeshConnection(false)`

The connections are saved into the file `AddOns/Movement/OffMeshConnectionsDatabase.lua`.

#### How it looks

Step 1 and 2:

![Step 1 and 2](images/improving-the-mesh/WoWScrnShot_111822_165827.jpg)

Step 3 and 4:

![Step 3 and 4](images/improving-the-mesh/WoWScrnShot_111822_165839.jpg)

Step 5:

![Step 5](images/improving-the-mesh/WoWScrnShot_111822_165855.jpg)

### Removing a connection

The connection with the closest `from` or `to` point, which is highlighted in a brighter blue, can be removed with `/script removeClosestOffMeshConnection()`.
