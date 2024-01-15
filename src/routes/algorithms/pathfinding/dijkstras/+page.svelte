<script>
	import { websiteName } from '$lib/stores';
	import P5 from 'p5-svelte';
	import { CodeBlock } from 'svhighlight';
	import { onDestroy } from 'svelte';

	let p5ref = undefined;

	let wallCount = 0;
	let nodesExpanded = 0;

	let pathfindingState = 'Running...';

	let w = 400;
	let h = 400;
	let cols = 20;
	let rows = 20;
	let grid = new Array(cols);

	let openSet = [];
	let closedSet = [];
	let start;
	let end;
	let path = [];
	let shortestPath = [];

	let width = w / cols;
	let height = h / rows;

	let sketch = function (p) {
		class Spot {
			constructor(i, j) {
				this.i = i;
				this.j = j;
				this.f = 0;
				this.g = 0;
				this.h = 0;
				this.neighbors = [];
				this.previous = undefined;
				this.wall = false;

				if (p.random(1) < 0.3) {
					this.wall = true;
					wallCount++;
				}
			}

			show(col) {
				p.fill(col);
				if (this.wall) {
					p.fill(0);
				}
				p.noStroke();
				p.rect(this.i * width, this.j * height, width - 1, height - 1);
			}

			addNeighbors(grid) {
				let i = this.i;
				let j = this.j;
				if (i < cols - 1) {
					this.neighbors.push(grid[i + 1][j]);
				}
				if (i > 0) {
					this.neighbors.push(grid[i - 1][j]);
				}
				if (j < rows - 1) {
					this.neighbors.push(grid[i][j + 1]);
				}
				if (j > 0) {
					this.neighbors.push(grid[i][j - 1]);
				}
				if (i > 0 && j > 0) {
					this.neighbors.push(grid[i - 1][j - 1]);
				}
				if (i < cols - 1 && j > 0) {
					this.neighbors.push(grid[i + 1][j - 1]);
				}
				if (i > 0 && j < rows - 1) {
					this.neighbors.push(grid[i - 1][j + 1]);
				}
				if (i < cols - 1 && j < rows - 1) {
					this.neighbors.push(grid[i + 1][j + 1]);
				}
			}
		}

		function setup() {
			p.createCanvas(w, h);
			p.background(255);

			for (let i = 0; i < cols; i++) {
				grid[i] = new Array(rows);
			}

			for (let i = 0; i < cols; i++) {
				for (let j = 0; j < rows; j++) {
					grid[i][j] = new Spot(i, j);
				}
			}

			for (let i = 0; i < cols; i++) {
				for (let j = 0; j < rows; j++) {
					grid[i][j].addNeighbors(grid);
				}
			}

			start = grid[0][0];
			end = grid[cols - 1][rows - 1];
			start.wall = false;
			end.wall = false;

			openSet.push(start);
		}

		function draw() {
			if (openSet.length > 0) {
				let winner = 0;
				for (let i = 0; i < openSet.length; i++) {
					if (openSet[i].f < openSet[winner].f) {
						winner = i;
					}
				}

				let current = openSet[winner];

				if (current === end) {
					p.noLoop();
					pathfindingState = 'Done!';

					// Find the shortest path
					let temp = end;
					shortestPath.push(temp);
					while (temp.previous) {
						shortestPath.push(temp.previous);
						temp = temp.previous;
					}

					// Draw the path
					p.noFill();
					p.stroke(0, 0, 255);
					p.strokeWeight(width / 2);
					p.beginShape();
					for (let i = shortestPath.length - 1; i >= 0; i--) {
						shortestPath[i].show(p.color(0, 0, 255));
						p.vertex(
							shortestPath[i].i * width + width / 2,
							shortestPath[i].j * height + height / 2
						);
					}
					p.endShape();
				}

				openSet = openSet.filter((spot) => spot !== current);
				closedSet.push(current);
				nodesExpanded++;

				let neighbors = current.neighbors;
				for (let i = 0; i < neighbors.length; i++) {
					let neighbor = neighbors[i];

					if (!closedSet.includes(neighbor) && !neighbor.wall) {
						let tempG = current.g + 1;

						if (!openSet.includes(neighbor)) {
							openSet.push(neighbor);
							neighbor.previous = current;
						}

						if (tempG < neighbor.g) {
							neighbor.g = tempG;
							neighbor.h = heuristic(neighbor, end);
							neighbor.f = neighbor.g + neighbor.h;

							if (!path.includes(neighbor)) {
								path.push(neighbor);
							}
						}
					}
				}
			} else {
				if (path.length === 0) {
					pathfindingState = 'No Solution';
					p.noLoop();
					return;
				}
			}

			p.background(255);

			for (let i = 0; i < cols; i++) {
				for (let j = 0; j < rows; j++) {
					grid[i][j].show(p.color(255));
				}
			}

			for (let i = 0; i < closedSet.length; i++) {
				closedSet[i].show(p.color(255, 0, 0));
			}

			// Draw the openSet in green
			for (let i = 0; i < openSet.length; i++) {
				openSet[i].show(p.color(0, 255, 0));
			}

			// Draw the path in blue
			for (let i = 0; i < path.length; i++) {
				path[i].show(p.color(0, 0, 255));
			}
		}

		p.setup = setup;
		p.draw = draw;
	};

	onDestroy(() => {
		if (p5ref) {
			p5ref.remove();
			p5ref = undefined;
		}
	});

	let reset = Math.random();

	// code block sections

	let codeLang = 'Python';

	$: code = `
	${
		codeLang === 'Python'
			? `
		# Python implementation of Dijkstra's algorithm

		# Class representing a node in the graph
		class Node:
			def __init__(self, name):
				self.name = name
				self.neighbors = []
				self.distance = float('inf')
				self.previous = None

			def add_neighbor(self, neighbor):
				self.neighbors.append(neighbor)

		# Class representing the graph
		class Graph:
			def __init__(self):
				self.nodes = []

			def add_node(self, node):
				self.nodes.append(node)

			def get_node(self, name):
				for node in self.nodes:
					if node.name == name:
						return node

			def get_nodes(self):
				return self.nodes

		# Dijkstra's algorithm
		def dijkstra(graph, start, end):
			start.distance = 0
			unvisited = set(graph.get_nodes())

			while len(unvisited) > 0:
				current = min(unvisited, key=lambda node: node.distance)
				unvisited.remove(current)

				for neighbor in current.neighbors:
					if neighbor in unvisited:
						distance = current.distance + 1
						if distance < neighbor.distance:
							neighbor.distance = distance
							neighbor.previous = current

			path = []
			current = end
			while current.previous:
				path.append(current)
				current = current.previous
			path.append(current)
			path.reverse()

			return path

		`
			: ''
	}
	${
		codeLang === 'C++'
			? `

		// C++ implementation of Dijkstra's algorithm

		#include <iostream>
		#include <vector>
		#include <queue>
		#include <unordered_map>
		#include <unordered_set>
		#include <limits>

		using namespace std;

		// Class representing a node in the graph
		class Node {
			public:
				string name;
				vector<Node*> neighbors;
				int distance;
				Node* previous;

				Node(string name) {
					this->name = name;
					this->distance = numeric_limits<int>::max();
					this->previous = nullptr;
				}

				void add_neighbor(Node* neighbor) {
					this->neighbors.push_back(neighbor);
				}
		};

		// Class representing the graph
		class Graph {
			public:
				vector<Node*> nodes;

				void add_node(Node* node) {
					this->nodes.push_back(node);
				}

				Node* get_node(string name) {
					for (Node* node : this->nodes) {
						if (node->name == name) {
							return node;
						}
					}
					return nullptr;
				}

				vector<Node*> get_nodes() {
					return this->nodes;
				}
		};

		// Dijkstra's algorithm
		vector<Node*> dijkstra(Graph* graph, Node* start, Node* end) {
			start->distance = 0;
			unordered_set<Node*> unvisited;
			for (Node* node : graph->get_nodes()) {
				unvisited.insert(node);
			}

			while (unvisited.size() > 0) {
				Node* current = *min_element(unvisited.begin(), unvisited.end(), [](Node* a, Node* b) {
					return a->distance < b->distance;
				});
				unvisited.erase(current);

				for (Node* neighbor : current->neighbors) {
					if (unvisited.find(neighbor) != unvisited.end()) {
						int distance = current->distance + 1;
						if (distance < neighbor->distance) {
							neighbor->distance = distance;
							neighbor->previous = current;
						}
					}
				}
			}

			vector<Node*> path;
			Node* current = end;
			while (current->previous) {
				path.push_back(current);
				current = current->previous;
			}
			path.push_back(current);
			reverse(path.begin(), path.end());

			return path;

		}
		
		`
			: ''
	}
	${
		codeLang === 'Java'
			? `

		// Java implementation of Dijkstra's algorithm

		import java.util.*;

		// Class representing a node in the graph
		class Node {
			public String name;
			public List<Node> neighbors;
			public int distance;
			public Node previous;

			public Node(String name) {
				this.name = name;
				this.neighbors = new ArrayList<>();
				this.distance = Integer.MAX_VALUE;
				this.previous = null;
			}

			public void addNeighbor(Node neighbor) {
				this.neighbors.add(neighbor);
			}
		}

		// Class representing the graph
		class Graph {
			public List<Node> nodes;

			public Graph() {
				this.nodes = new ArrayList<>();
			}

			public void addNode(Node node) {
				this.nodes.add(node);
			}

			public Node getNode(String name) {
				for (Node node : this.nodes) {
					if (node.name.equals(name)) {
						return node;
					}
				}
				return null;
			}

			public List<Node> getNodes() {
				return this.nodes;
			}
		}

		// Dijkstra's algorithm
		public List<Node> dijkstra(Graph graph, Node start, Node end) {
			start.distance = 0;
			Set<Node> unvisited = new HashSet<>(graph.getNodes());

			while (unvisited.size() > 0) {
				Node current = Collections.min(unvisited, Comparator.comparing(node -> node.distance));
				unvisited.remove(current);

				for (Node neighbor : current.neighbors) {
					if (unvisited.contains(neighbor)) {
						int distance = current.distance + 1;
						if (distance < neighbor.distance) {
							neighbor.distance = distance;
							neighbor.previous = current;
						}
					}
				}
			}

			List<Node> path = new ArrayList<>();
			Node current = end;
			while (current.previous != null) {
				path.add(current);
				current = current.previous;
			}
			path.add(current);
			Collections.reverse(path);

			return path;
		}

		`
			: ''
	}
	${
		codeLang === 'Go'
			? `
		// GoLang implementation of Dijkstra's algorithm

		package main

		import (
			"fmt"
			"math"
		)

		// Node represents a node in the graph
		type Node struct {
			name     string
			neighbors []*Node
			distance int
			previous *Node
		}

		// Graph represents a graph
		type Graph struct {
			nodes []*Node
		}

		// AddNode adds a node to the graph
		func (g *Graph) AddNode(node *Node) {
			g.nodes = append(g.nodes, node)
		}

		// GetNode returns a node in the graph
		func (g *Graph) GetNode(name string) *Node {
			for _, node := range g.nodes {
				if node.name == name {
					return node
				}
			}
			return nil
		}

		// GetNodes returns all nodes in the graph
		func (g *Graph) GetNodes() []*Node {
			return g.nodes
		}

		// Dijkstra returns the shortest path between two nodes
		func Dijkstra(graph *Graph, start *Node, end *Node) []*Node {
			start.distance = 0
			unvisited := make(map[*Node]bool)
			for _, node := range graph.GetNodes() {
				unvisited[node] = true
			}

			for len(unvisited) > 0 {
				var current *Node
				for node := range unvisited {
					if current == nil || node.distance < current.distance {
						current = node
					}
				}
				delete(unvisited, current)

				for _, neighbor := range current.neighbors {
					if unvisited[neighbor] {
						distance := current.distance + 1
						if distance < neighbor.distance {
							neighbor.distance = distance
							neighbor.previous = current
						}
					}
				}
			}

			path := []*Node{}
			current := end
			for current.previous != nil {
				path = append(path, current)
				current = current.previous
			}
			path = append(path, current)
			reverse(path)

			return path
		}

		// reverse reverses a slice of nodes
		func reverse(nodes []*Node) {
			for i := 0; i < len(nodes)/2; i++ {
				j := len(nodes) - i - 1
				nodes[i], nodes[j] = nodes[j], nodes[i]
			}
		}

		// main function
		func main() {
			graph := Graph{}

			// Create nodes
			a := Node{name: "A"}
			b := Node{name: "B"}
			c := Node{name: "C"}
			d := Node{name: "D"}
			e := Node{name: "E"}
			f := Node{name: "F"}
			g := Node{name: "G"}
			h := Node{name: "H"}

			// Add neighbors
			a.neighbors = []*Node{&b, &c}
			b.neighbors = []*Node{&a, &d}
			c.neighbors = []*Node{&a, &d, &e}
			d.neighbors = []*Node{&b, &c, &f}
			e.neighbors = []*Node{&c, &f, &g}
			f.neighbors = []*Node{&d, &e, &h}
			g.neighbors = []*Node{&e, &h}
			h.neighbors = []*Node{&f, &g}

			// Add nodes to graph
			graph.AddNode(&a)
			graph.AddNode(&b)
			graph.AddNode(&c)
			graph.AddNode(&d)
			graph.AddNode(&e)
			graph.AddNode(&f)
			graph.AddNode(&g)
			graph.AddNode(&h)

			// Find shortest path
			path := Dijkstra(&graph, &a, &h)

			// Print shortest path
			for _, node := range path {
				fmt.Printf("%s ", node.name)
			}
			fmt.Println()
		}

		`
			: ''
	}
	`.trim();
</script>

<svelte:head>
	<title>Dijkstra's Algorithm - {websiteName}</title>
</svelte:head>

<div class="container mx-auto mb-20">
	<!-- Title -->
	<div class="flex justify-center items-center px-20">
		<h1 class="text-6xl font-bold white">Dijkstra's Pathfinding Algorithm</h1>
	</div>
</div>

<div class="container mx-auto">
	<div class="md:flex md:justify-center md:space-x-4">
		<!-- Section for Algorithm Properties -->
		<div
			class="mx-4 p-4 py-20 h-100 border border-gray-500 rounded-lg shadow-xl mb-4 md:mb-0 md:mx-0 sm:mb-4 overflow-hidden my-auto"
			style="background-color: #141414;"
		>
			<p class="text-base font-semibold text-gray-100 text-center">Performance</p>
			<div class="flex-col justify-between mt-2">
				<div class="mb-1">
					<div class="inline-flex items-center">
						<p class="text-base text-gray-200">Time Complexity:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">
						O(|V|<sup>2</sup>)
					</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center">
						<p class="text-base text-gray-200">Space Complexity:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">O(|V|)</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center">
						<p class="text-base text-gray-200">Search Countours:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">Uniform</p>
				</div>
				<div class="mb-1">
					<p class="text-xs text-gray-200 mt-2">
						What are <a
							href={'/algorithms#pathfinding-algorithms'}
							class="text-blue-400 hover:text-blue-300">Search contours</a
						>?
					</p>
				</div>
			</div>
		</div>

		<!-- Section for Animation -->
		<div
			class="w-100 h-100 border border-gray-500 rounded-lg shadow-xl overflow-hidden relative mb-4 md:mb-0 md:mr-4 sm:mb-4 mt-4"
		>
			<div class="flex items-center justify-center">
				{#key reset}
					<P5 {sketch} />
				{/key}
			</div>
		</div>

		<!-- Section for Real-time pathfinding statistics -->
		<div
			class="mx-4 p-4 py-20 h-100 border border-gray-500 rounded-lg shadow-xl mb-4 md:mb-0 md:mr-4 sm:mb-4 overflow-hidden my-auto"
			style="background-color: #141414;"
		>
			<p class="text-base font-semibold text-gray-100 text-center">Pathfinding Stats</p>
			<div class="flex-col justify-between mt-2">
				<div class="mb-1">
					<div class="inline-flex items-center">
						<span class="inline-block text-xs mr-1">⏳</span>
						<p class="text-base text-gray-200">Status</p>
					</div>
					<p class="text-xl font-bold text-blue-600">{pathfindingState}</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center">
						<span class="w-2 h-2 inline-block rounded-full me-2" style="background-color: #57ce00;"
						></span>
						<p class="text-base text-gray-200">Visited Node Count:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">{nodesExpanded}</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center">
						<span class="w-2 h-2 inline-block rounded-full me-2" style="background-color: #0000ff;"
						></span>
						<p class="text-base text-gray-200">Path Length:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">N/A</p>
				</div>
				<div class="mb-1">
					<p class="text-xs text-gray-200 mt-2">Grid size: {rows} x {cols}, Walls: {wallCount}</p>
				</div>
			</div>
		</div>
	</div>
</div>

<div class="container py-8 items-center justify-center mx-auto">
	<div class="container py-8 flex items-center justify-center mx-auto">
		<button
			class="w-48 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded text-center"
			on:click={() => {
				reset = Math.random();
				pathfindingState = 'Running...';
				nodesExpanded = 0;
				wallCount = 0;

				if (p5ref) {
					p5ref.remove();
					p5ref = undefined;
				}
			}}
		>
			Reset
		</button>
	</div>

	<div class="py-8">
		<p class="text-xs text-white mt-2 text-center">
			⚠️ <span class="font-bold">Note:</span> this animated visualization is a work-in-progress. If you
			are encountering errors or want to replay the animation, please refresh the page.
		</p>
		<p class="text-xs text-white mt-2 text-center">
			If you would like to report a bug or suggest an improvement, please create an issue on
			<a
				href={'https://github.com/Verdone/swe-insight/issues'}
				target="_blank"
				class="text-blue-500 hover:text-blue-300">GitHub</a
			>.
		</p>
	</div>
</div>

<section class="bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">
				Understanding Dijkstra's Algorithm
			</h2>
			<p class="mb-4 font-light">
				Arguably one of the most popular pathfinding algorithms, Dijkstra's algorithm is a weighted
				algorithm that finds the shortest path between two nodes in a graph. While it visits all
				nodes in the graph, it guaranteed to find the shortest path.
			</p>

			<p class="mb-4 font-light">
				To understand how Dijkstra's algorithm works, we must first understand the concept of a
				<span class="font-bold">weighted graph</span>. A weighted graph is a graph where each edge
				has a weight or cost associated with it. For example, in the graph below, the edge between
				node A and B has a weight of 2, while the edge between node B and C has a weight of 3. The
				weight of an edge represents the cost of traversing that edge. In the context of
				pathfinding, the weight of an edge represents the distance between two nodes. For example,
				if we were to represent a graph as a map, the weight of an edge would represent the distance
				between two cities.
			</p>

			<p class="mb-10 font-light">
				Now that we understand what a weighted graph is, we can begin to understand how Dijkstra's
				algorithm works. Dijkstra's algorithm works by visiting each node in the graph and
				calculating the shortest distance from the starting node to that node. It does this by
				keeping track of the
				<span class="font-bold">shortest distance</span> from the starting node to each node in the graph.
				Initially, the shortest distance from the starting node to all other nodes is set to infinity.
				Then, the algorithm begins to visit each node in the graph. For each node, the algorithm checks
				each of its neighbors and calculates the distance from the starting node to that neighbor. If
				the calculated distance is less than the current shortest distance, the shortest distance is
				updated to the calculated distance. This process is repeated until all nodes in the graph have
				been visited.
			</p>
		</div>
	</div>
</section>

<section class="bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Code Implementation</h2>
			<p class="mb-4 font-medium">
				Dijkstra's pathfinding algorithm can be implemented in a variety of languages. Below are
				some examples of implementations in Python, C++, Go, and Java.
			</p>

			<!-- Code block language selection buttons -->
			<div class="flex justify-center items-center space-x-4 mb-4">
				<button
					on:click={() => (codeLang = 'Python')}
					class="w-24 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
				>
					Python
				</button>
				<button
					on:click={() => (codeLang = 'C++')}
					class="w-24 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
				>
					C++
				</button>
				<button
					on:click={() => (codeLang = 'Java')}
					class="w-24 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
				>
					Java
				</button>
				<button
					on:click={() => (codeLang = 'Go')}
					class="w-24 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
				>
					GoLang
				</button>
			</div>

			<div class="shadow-2xl mb-10">
				{#key codeLang}
					<CodeBlock language={codeLang} {code} />
				{/key}
			</div>

			<p class="text-xs text-gray-200 mt-2">
				Note: these implementations are for educational purposes only, such as preparing for a
				technical interview or for learning about sorting algorithms. They are not intended to be
				used in production as-is, as they may not be optimized.
			</p>
		</div>
	</div>
</section>
