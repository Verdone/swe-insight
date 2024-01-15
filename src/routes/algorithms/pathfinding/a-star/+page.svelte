<script>
	import { websiteName } from '$lib/stores';
	import P5 from 'p5-svelte';
	import { CodeBlock } from 'svhighlight';
	import { onDestroy } from 'svelte';

	let p5ref = undefined;
	let w = 400;
	let h = 400;
	let cols = 20;
	let rows = 20;
	let grid = new Array(cols);

	let openSet = [];
	let closedSet = [];
	let start;
	let end;
	let wall = [];
	let path = [];

	let width = w / cols;
	let height = h / rows;
	let wallCount = 0;
	let nodesExpanded = 0;

	let pathfindingState = 'Running...';

	let sketch = function (p) {
		function removeFromArray(arr, elt) {
			for (let i = arr.length - 1; i >= 0; i--) {
				if (arr[i] == elt) {
					arr.splice(i, 1);
				}
			}
		}

		function heuristic(a, b) {
			let d = p.dist(a.i, a.j, b.i, b.j);
			return d;
		}

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
			let current;

			if (openSet.length > 0) {
				let winner = 0;
				for (let i = 0; i < openSet.length; i++) {
					if (openSet[i].f < openSet[winner].f) {
						winner = i;
					}
				}

				current = openSet[winner];

				if (current === end) {
					p.noLoop();
					pathfindingState = 'Completed!';
				}

				removeFromArray(openSet, current);
				closedSet.push(current);
				nodesExpanded++;

				let neighbors = current.neighbors;
				for (let i = 0; i < neighbors.length; i++) {
					let neighbor = neighbors[i];

					if (!closedSet.includes(neighbor) && !neighbor.wall) {
						let tempG = current.g + 1;

						let newPath = false;
						if (openSet.includes(neighbor)) {
							if (tempG < neighbor.g) {
								neighbor.g = tempG;
								newPath = true;
							}
						} else {
							neighbor.g = tempG;
							newPath = true;
							openSet.push(neighbor);
						}

						if (newPath) {
							neighbor.h = heuristic(neighbor, end);
							neighbor.f = neighbor.g + neighbor.h;
							neighbor.previous = current;
						}
					}
				}
			} else {
				pathfindingState = 'No Solution.';
				p.noLoop();
				return;
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

			for (let i = 0; i < openSet.length; i++) {
				openSet[i].show(p.color(0, 255, 0));
			}

			path = [];
			let temp = current;
			path.push(temp);
			while (temp.previous) {
				path.push(temp.previous);
				temp = temp.previous;
			}

			for (let i = 0; i < path.length; i++) path[i].show(p.color(0, 0, 255));

			p.noFill();

			p.stroke(255, 0, 200);
			p.strokeWeight(width / 2);
			p.beginShape();
			for (let i = 0; i < path.length; i++) {
				p.vertex(path[i].i * width + width / 2, path[i].j * height + height / 2);
			}
			p.endShape();
		}

		p.setup = setup;
		p5ref = p;
		p.draw = draw;
	};

	onDestroy(() => {
		if (p5ref) {
			p5ref.remove();
			p5ref = undefined;
		}
	});

	let reset = Math.random();

	$: wallCount;
	$: nodesExpanded;

	// code block sections

	let codeLang = 'Python';

	$: code = `
        ${
					codeLang === 'Python'
						? `
        def a_star_search(graph, start, goal):
            frontier = PriorityQueue()
            frontier.put(start, 0)
            came_from = {}
            cost_so_far = {}
            came_from[start] = None
            cost_so_far[start] = 0

            while not frontier.empty():
                current = frontier.get()

                if current == goal:
                    break

                for next in graph.neighbors(current):
                    new_cost = cost_so_far[current] + graph.cost(current, next)
                    if next not in cost_so_far or new_cost < cost_so_far[next]:
                        cost_so_far[next] = new_cost
                        priority = new_cost + heuristic(goal, next)
                        frontier.put(next, priority)
                        came_from[next] = current

            return came_from, cost_so_far
        `
						: ''
				}
        ${
					codeLang === 'C++'
						? `
        void a_star_search(Graph graph, Node start, Node goal) {
            PriorityQueue frontier;
            frontier.put(start, 0);
            came_from = {};
            cost_so_far = {};
            came_from[start] = NULL;
            cost_so_far[start] = 0;

            while (!frontier.empty()) {
                current = frontier.get();

                if (current == goal) {
                    break;
                }

                for (next in graph.neighbors(current)) {
                    new_cost = cost_so_far[current] + graph.cost(current, next);
                    if (next not in cost_so_far || new_cost < cost_so_far[next]) {
                        cost_so_far[next] = new_cost;
                        priority = new_cost + heuristic(goal, next);
                        frontier.put(next, priority);
                        came_from[next] = current;
                    }
                }
            }

            return came_from, cost_so_far;
        }
        `
						: ''
				}
        ${
					codeLang === 'Java'
						? `
        public static void a_star_search(Graph graph, Node start, Node goal) {

            PriorityQueue<Node> frontier = new PriorityQueue<Node>();
            frontier.put(start, 0);
            came_from = new HashMap<Node, Node>();
            cost_so_far = new HashMap<Node, Integer>();
            came_from.put(start, null);
            cost_so_far.put(start, 0);

            while (!frontier.empty()) {
                Node current = frontier.get();

                if (current == goal) {
                    break;
                }

                for (Node next : graph.neighbors(current)) {
                    int new_cost = cost_so_far.get(current) + graph.cost(current, next);
                    if (!cost_so_far.containsKey(next) || new_cost < cost_so_far.get(next)) {
                        cost_so_far.put(next, new_cost);
                        int priority = new_cost + heuristic(goal, next);
                        frontier.put(next, priority);
                        came_from.put(next, current);
                    }
                }
            }

            return came_from, cost_so_far;
        }
        `
						: ''
				}
        ${
					codeLang === 'Go'
						? `
        func a_star_search(graph Graph, start Node, goal Node) {
            frontier := PriorityQueue{}
            frontier.put(start, 0)
            came_from := map[Node]Node{}
            cost_so_far := map[Node]int{}
            came_from[start] = nil
            cost_so_far[start] = 0

            for !frontier.empty() {
                current := frontier.get()

                if current == goal {
                    break
                }

                for _, next := range graph.neighbors(current) {
                    new_cost := cost_so_far[current] + graph.cost(current, next)
                    if _, ok := cost_so_far[next]; !ok || new_cost < cost_so_far[next] {
                        cost_so_far[next] = new_cost
                        priority := new_cost + heuristic(goal, next)
                        frontier.put(next, priority)
                        came_from[next] = current
                    }
                }
            }

            return came_from, cost_so_far
        }
        `
						: ''
				}
    `;
</script>

<svelte:head>
	<title>A* Star Algorithm - {websiteName}</title>
</svelte:head>

<div class="container mx-auto mb-20">
	<!-- Title -->
	<div class="flex justify-center items-center px-20">
		<h1 class="text-6xl font-bold white">A* Star Pathfinding Algorithm</h1>
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
					<p class="text-xl font-bold text-blue-600">Varies</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center">
						<p class="text-base text-gray-200">Space Complexity:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">Varies</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center">
						<p class="text-base text-gray-200">Search Countours:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">Stretched</p>
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
					<p class="text-xl font-bold text-blue-600">{path.length}</p>
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

<!-- Section 1: Explanation of the Algorithm -->
<section class="bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Understanding A* Star</h2>
			<p class="mb-4 font-light">
				A* operates on a graph or a grid where each node represents a point in space, and edges
				represent possible transitions between nodes. The algorithm requires information about the
				cost of moving from one node to another and a heuristic function that estimates the cost
				from a given node to the goal.
			</p>

			<p class="mb-4 font-light">
				A priority queue (often implemented using a min-heap) is used to keep track of the nodes to
				be explored. Nodes are prioritized based on their total cost.
			</p>

			<p class="mb-10 font-light">
				To implement this sorting algorithm, we initialize the start node and add it to the priority
				queue with a priority value of the heuristic estimate from the start to the goal. Set the
				cost to reach the start node as 0. While the priority queue is not empty, we remove the node
				with the lowest priority value from the queue and mark it as visited. If the node is the
				goal, we have found the shortest path. Otherwise, we add all of the node's neighbors to the
				priority queue with a priority value of the cost to reach the current node plus the
				heuristic estimate from the neighbor to the goal. If the neighbor is already in the priority
				queue, we update its priority value if the new value is lower than the old one. Finally, the
				algorithm terminates when the priority queue is empty or the goal node is removed from the
				queue.
			</p>
		</div>
	</div>
</section>

<section class="bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Code Implementation</h2>
			<p class="mb-4 font-medium">
				A* Star can be implemented in a variety of languages. Below are some examples of
				implementations in Python, C++, Go, and Java.
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
