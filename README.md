# tableau-networks
Tableau graphs and network structures tutorial with export support for Python's NetworkX graph package.

## Graph Structures in Tableau: A Tutorial
When uploading graphs into tableau, they can be in table format as long as they are structured correctly. Nodes and edges must be saved in separate files.
### Node File
#### Required Columns:
Node tables in Tableau require the following columns.
* **Node IDs**: These are unique identifiers for each node, and they act as a key. Ideally they are a discrete dimension. Ending the column name with "\_Id" such as `Node_Id` will ensure it gets treated as a dimension when uploaded to tableau.
* **X coordinate**: The position on the x-axis for each node, probably a decimal number. Ideally they are a continuous dimension. Ending the column name with "\_Nbr" such as `x_Nbr` will ensure it gets treated as a dimension when uploaded to tableau.
* **Y coordinate**: The position on the y-axis for each node, probably a decimal number. Ideally they are a continuous dimension. Ending the column name with "\_Nbr" such as `y_Nbr` will ensure it gets treated as a dimension when uploaded to tableau.

#### Optional Columns:
Optional columns you could put in node files include, but are not limited to:
* Shape of node: Square, Circle, Cross, etc.
* Color of node: Explicit color names or some other value you wish to color the node with.
* Size of node: Scaling the size of the node is an option, but I caution you to keep them all within a magnitude of 10 for visual purposes.
* Label of node: Short text that stays as a node label.
* Long text of node: Longer text that can be included in a tooltip.
* Filterable properties for a node: detail that can be used to filter a node.

### Edge File
#### Required Columns:
Edge tables in Tableau have two rows per edge, one "from" row and one "to" row. Each Edge has a unique Edge ID shared by the "from" row and the "to" row. Each from and to row contain a node ID for the node that the edge starts or ends at, respectively. The tableau graph will be undirected so it does not matter which order they are in.

* **Edge IDs**: These are unique identifiers for each edge, but they do not act as a key. Ideally they are a discrete dimension. Ending the column name with "\_Id" such as `Edge_Id` will ensure it gets treated as a dimension when uploaded to tableau. A single Edge ID appears twice: once in the "from" row, and again in the "to" row.
* **Node IDs**: The Node ID column contains Node ID values from the Node table. In the "from" row, the Node ID is the ID of the node the edge starts at. In the "to" row, the Node ID is the ID of the node the edge ends at.

In the case of the graph:

(Node A) --Edge 0-- (Node B) --Edge 1-- (Node C)

The bare-bones Edge Table looks like this:

| edge_id |  node_id |
| ------- | -------- |
|    0    | A        |
|    0    | B        |
|    1    | B        |
|    1    | C        |

#### Recommended Columns:
* **Row Type**: something to indicate whether the row in the edge table is a "from" row or a "to" row, for readability

#### Optional Columns:
Edge options should be shared across both "from" and "to" rows. Optional columns you could put in edge files include, but are not limited to:
* Weight of edge: How wide should the edge be?
* Color of edge: Explicit color names or some other value you wish to color the edge with.
* Label of edge: Short text that stays as a edge label.
* Long text of edge: Longer text that can be included in a tooltip.
