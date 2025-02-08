Flow JSON Specification  
Version 1.1 — 2025-01-12

## Top Level
The Flow JSON format consists of the following arrays:

1. **nodes** (required, array of node objects): Represents the graphical elements on the canvas.  
2. **edges** (required, array of edge objects): Represents the connections between nodes.  

---

## Nodes
Nodes represent the main visual and interactive elements.  

### Generic Node Properties
All nodes include the following attributes:
- **id** (required, string): Unique identifier for the node.  
- **position** (required, object): Coordinates of the node. Format: `{ x: number, y: number }`.  
- **data** (optional, object): Arbitrary data attached to the node.  
- **type** (optional, string): Type of the node. Default is "default". Other valid types include (`"input"`, `"output"`, `"group"`, and `"custom"`).
- **sourcePosition** (optional, string): The side of the node where connections originate (`"top"`, `"right"`, `"bottom"`, `"left"`).  
- **targetPosition** (optional, string): The side of the node where connections terminate.  
- **hidden** (optional, boolean): If `true`, the node is not displayed.  
- **selected** (optional, boolean): If `true`, the node is highlighted as selected.  
- **dragging** (optional, boolean): If `true`, the node is currently being dragged.  
- **draggable** (optional, boolean): If `false`, the node cannot be dragged.  
- **selectable** (optional, boolean): If `false`, the node cannot be selected.  
- **connectable** (optional, boolean): If `false`, the node cannot form connections.  
- **deletable** (optional, boolean): If `false`, the node cannot be deleted.  
- **width** (optional, number): Width of the node.  
- **height** (optional, number): Height of the node.  
- **parentId** (optional, string): ID of the parent node for nested structures.  
- **extent** (optional, string | array): Movement boundary, e.g., `"parent"` or `[[0, 0], [100, 100]]`.  
- **origin** (optional, array): Origin point of the node, e.g., `[0.5, 0.5]` centers the node.  
- **handles** (optional, array of handles): Custom connection points.  
  - **source** (optional, array): Source handle configurations.  
  - **target** (optional, array): Target handle configurations.  

### Internal Properties (Generated during runtime)
- **positionAbsolute** (object): The node's absolute position `{ x: number, y: number }`.  
- **zIndex** (number): Stacking order of the node.  
- **bounds** (object): The node's boundaries `{ x: number, y: number, width: number, height: number }`.  

---

## Edges
Edges represent connections between nodes.

### Generic Edge Properties
- **id** (required, string): Unique identifier for the edge.  
- **source** (required, string): ID of the source node.  
- **target** (required, string): ID of the target node.  
- **sourceHandle** (optional, string): ID of the source handle.  
- **targetHandle** (optional, string): ID of the target handle.  
- **label** (optional, string): Text label for the edge.  
- **animated** (optional, boolean): If `true`, the edge is rendered with animation.  
- **style** (optional, object): Custom style object for the edge.  
- **selected** (optional, boolean): If `true`, the edge is highlighted as selected.  

---

## Handles
Handles are custom connection points for nodes.  
Each handle includes the following attributes:
- **id** (required, string): Unique identifier for the handle.  
- **type** (required, string): Handle type (`"source"` or `"target"`).  
- **position** (required, string): Handle position relative to the node (`"top"`, `"right"`, `"bottom"`, `"left"`).  
- **width** (optional, number): Width of the handle.  
- **height** (optional, number): Height of the handle.  

---

## Usage Notes
This comprehensive schema supports advanced features like nested nodes, precise node positioning, dynamic handles, and animated edges, making it ideal for interactive and visually rich canvas-based applications.


## Example
Here’s an example of a Svelte Flow JSON object:

{
  "nodes": [
    {
      "id": "node-1",
      "type": "default",
      "position": { "x": 100, "y": 200 },
      "data": { "label": "Node 1" },
      "sourcePosition": "right",
      "targetPosition": "left",
      "hidden": false,
      "selected": false,
      "dragging": false,
      "draggable": true,
      "selectable": true,
      "connectable": true,
      "deletable": true,
      "width": 150,
      "height": 50,
      "parentId": null,
      "extent": "parent",
      "origin": [0.5, 0.5],
      "handles": [
        { "id": "handle-1", "type": "source", "position": "right" },
        { "id": "handle-2", "type": "target", "position": "left" }
      ]
    },
    {
      "id": "node-2",
      "type": "input",
      "position": { "x": 400, "y": 200 },
      "data": { "label": "Node 2" },
      "sourcePosition": "top",
      "targetPosition": "bottom",
      "hidden": false,
      "selected": true,
      "dragging": false,
      "draggable": true,
      "selectable": true,
      "connectable": true,
      "deletable": true,
      "width": 150,
      "height": 50,
      "parentId": "node-1",
      "extent": [[0, 0], [800, 600]],
      "origin": [0, 0]
    }
  ],
  "edges": [
    {
      "id": "edge-1",
      "source": "node-1",
      "target": "node-2",
      "sourceHandle": "handle-1",
      "targetHandle": null,
      "label": "Edge from Node 1 to Node 2",
      "animated": true,
      "style": { "stroke": "#FF0000", "strokeWidth": 2 },
      "selected": false
    }
  ]
}
