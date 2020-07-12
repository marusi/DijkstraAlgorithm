# Dijkstra Algorithm



> Dijkstra's algorithm is an algorithm for finding the shortest paths between nodes in a graph. [wikipedia](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)

## Github URL
https://github.com/marusi/DijkstraAlgorithm

## Nuget Packages

| Nuget Package Name | Nuget Package URL                                                  |
|--------------------|--------------------------------------------------------------------|
| DijkstraAlgorithm  | COMING SOON |

## Example Usage

``` C#
// Create graph --- new object from GraphBuilder Class
var newGraph = new GraphBuilder();
// add node or vertices: Tokyo, Moscow, Berlin, Nairobi, Rio, Denver, Helsinki, and Oslo.
newGraph.AddNode("Nairobi"); //a
newGraph.AddNode("Tokyo");   //b
newGraph.AddNode("Moscow");  // c
newGraph.AddNode("Berlin");  //d
newGraph.AddNode("Rio");     //e
newGraph.AddNode("Denver");  //f
newGraph.AddNode("Helsinki"); //g
newGraph.AddNode("Oslo");    //h

// Link Added and its relative cost
// newGraph.AddLink("Origin", "Destination", cost.inDouble... ) if you prefer decimal... later convert to double

newGraph
    .AddLink("Nairobi", "Tokyo", 600)
    .AddLink("Nairobi", "Berlin", 100);

newGraph
    .AddLink("Tokyo", "Nairobi", 600)
    .AddLink("Tokyo", "Moscow", 500)
    .AddLink("Tokyo", "Berlin", 200)
    .AddLink("Tokyo", "Rio", 200);

builder
    .AddLink("Moscow", "Tokyo", 500)
    .AddLink("Moscow", "Rio", 500);

builder
    .AddLink("Berlin", "Nairobi", 100)
    .AddLink("Berlin", "Tokyo", 200)
    .AddLink("Berlin", "Rio", 100);

builder
    .AddLink("Rio", "Tokyo", 200)
    .AddLink("Rio", "Moscow", 500)
    .AddLink("Rio", "Berlin", 100);

// call the Build Method
var graph = newGraph.Build();

// Create path finder
var pathFinder = new PathFinder(graph);

// Find path
const string origin = "Nairobi", destination = "Moscow";

var path = pathFinder.FindShortestPath(
    graph.Nodes.Single(node => node.Id == origin),
    graph.Nodes.Single(node => node.Id == destination));

// Assert results
Assert.Equal(path.Origin.Id, origin);
Assert.Equal(path.Destination.Id, destination);
Assert.Equal(path.Segments.Count, 300);
Assert.Equal(path.Segments.Sum(s => s.Weight), 700);

Assert.Equal(path.Segments.ElementAt(0).Origin.Id, "Nairobi");
Assert.Equal(path.Segments.ElementAt(0).Weight, 100);
Assert.Equal(path.Segments.ElementAt(0).Destination.Id, "Berlin");

Assert.Equal(path.Segments.ElementAt(1).Origin.Id, "Berlin");
Assert.Equal(path.Segments.ElementAt(1).Weight, 100);
Assert.Equal(path.Segments.ElementAt(1).Destination.Id, "Rio");

Assert.Equal(path.Segments.ElementAt(2).Origin.Id, "Rio");
Assert.Equal(path.Segments.ElementAt(2).Weight, 500);
Assert.Equal(path.Segments.ElementAt(2).Destination.Id, "Moscow");
```
