<script>
	import { websiteName } from '$lib/stores';
	import { CodeBlock } from 'svhighlight';

	let codeLang = 'Python';

	$: code = `
		${
			codeLang === 'Python'
				? `
class Queue:
	def __init__(self):
		self.items = []

	def is_empty(self):
		return len(self.items) == 0

	def enqueue(self, item):
		self.items.append(item)

	def dequeue(self):
		if not self.is_empty():
			return self.items.pop(0)
		else:
			return None

	def size(self):
		return len(self.items)
            `
				: ''
		}
        ${
					codeLang === 'C++'
						? `
class Queue {
    private:
        int front, rear, size;
        unsigned capacity;
        int* array;
    public:
        Queue(unsigned capacity) {
            this->capacity = capacity;
            front = size = 0;
            rear = capacity - 1;
            array = new int[this->capacity];
        }

        bool is_full() {
            return (size == capacity);
        }

        bool is_empty() {
            return (size == 0);
        }

        void enqueue(int item) {
            if (is_full()) {
                return;
            }
            rear = (rear + 1) % capacity;
            array[rear] = item;
            size++;
        }

        int dequeue() {
            if (is_empty()) {
                return INT_MIN;
            }
            int item = array[front];
            front = (front + 1) % capacity;
            size--;
            return item;
        }

        int get_front() {
            if (is_empty()) {
                return INT_MIN;
            }
            return array[front];
        }

        int get_rear() {
            if (is_empty()) {
                return INT_MIN;
            }
            return array[rear];
        }
};
            `
						: ''
				}
        ${
					codeLang === 'Java'
						? `
class Queue {
    private int front, rear, size;
    private int capacity;
    private int[] array;

    public Queue(int capacity) {
        this.capacity = capacity;
        front = size = 0;
        rear = capacity - 1;
        array = new int[this.capacity];
    }

    public boolean is_full() {
        return (size == capacity);
    }

    public boolean is_empty() {
        return (size == 0);
    }

    public void enqueue(int item) {
        if (is_full()) {
            return;
        }
        rear = (rear + 1) % capacity;
        array[rear] = item;
        size++;
    }

    public int dequeue() {
        if (is_empty()) {
            return Integer.MIN_VALUE;
        }
        int item = array[front];
        front = (front + 1) % capacity;
        size--;
        return item;
    }

    public int get_front() {
        if (is_empty()) {
            return Integer.MIN_VALUE;
        }
        return array[front];
    }

    public int get_rear() {
        if (is_empty()) {
            return Integer.MIN_VALUE;
        }
        return array[rear];
    }
}
            `
						: ''
				}
        ${
					codeLang === 'Go'
						? ` 
type Queue struct {
    items []int
}

func (q *Queue) is_empty() bool {
    return len(q.items) == 0
}

func (q *Queue) enqueue(item int) {
    q.items = append(q.items, item)
}

func (q *Queue) dequeue() int {
    if !q.is_empty() {
        item := q.items[0]
        q.items = q.items[1:]
        return item
    } else {
        return -1
    }
}

func (q *Queue) size() int {
    return len(q.items)
}
            `
						: ''
				}
    `;
</script>

<svelte:head>
	<title>Queues - {websiteName}</title>
</svelte:head>

<div class="container mx-auto mb-20">
	<!-- Title -->
	<div class="flex justify-center items-center px-20 py-20">
		<h1 class="text-6xl font-bold white">Queue Data Structure</h1>
	</div>
</div>

<!-- Section 1: Explanation of the Data Structure -->
<section class="bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">
				Understanding the Queue Data Structure
			</h2>
			<p class="mb-4 font-light">
				A Queue is a linear data structure that follows the First In, First Out (FIFO) principle.
				Elements are added to the rear (enqueue) and removed from the front (dequeue). It models a
				real-world queue or line where the first person to join is the first to be served.
			</p>
			<p class="mb-10 font-light">
				The basic operations on a Queue include enqueue (adding an element to the rear), dequeue
				(removing an element from the front), is_empty (checking if the queue is empty), and size
				(determining the number of elements in the queue).
			</p>
		</div>
	</div>
</section>

<!-- Section 2: Complexity Analysis for Queue -->
<section class="bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Complexity Analysis</h2>
			<p class="mb-4 font-medium">
				A queue can have the following complexities, however its performance is dependent on the
				underlying data structure used to implement it:
			</p>

			<div class="relative overflow-x-auto mb-4">
				<table class="w-full text-sm text-left rtl:text-right text-gray-400">
					<thead class="text-xs uppercase bg-gray-900 text-gray-400">
						<tr>
							<th scope="col" class="px-6 py-3"> Case </th>
							<th scope="col" class="px-6 py-3"> Time Complexity </th>
							<th scope="col" class="px-6 py-3"> Space Complexity </th>
						</tr>
					</thead>
					<tbody>
						<tr class="border-b bg-gray-950 border-gray-700">
							<th scope="row" class="px-6 py-4 font-medium whitespace-nowrap text-white">
								Best Case
							</th>
							<td class="px-6 py-4 text-gray-200">Ω(1)</td>
							<td class="px-6 py-4 text-gray-200">Ω(n)</td>
						</tr>
						<tr class="bg-gray-950 border-gray-700">
							<th scope="row" class="px-6 py-4 font-medium whitespace-nowrap text-white">
								Average Case
							</th>
							<td class="px-6 py-4 text-gray-200">Θ(n)</td>
							<td class="px-6 py-4 text-gray-200">Θ(1)</td>
						</tr>
						<tr class="bg-gray-950">
							<th scope="row" class="px-6 py-4 font-medium whitespace-nowrap text-white">
								Worst Case
							</th>
							<td class="px-6 py-4 text-gray-200">O(1)</td>
							<td class="px-6 py-4 text-gray-200">O(n)</td>
						</tr>
					</tbody>
				</table>
			</div>

			<p class="mb-4 font-medium">
				Queues are particularly efficient when constant-time enqueue and dequeue operations are
				critical. If you'd like to write a program that simulates when to use a queue, check out
				LeetCode's <a
					href="https://leetcode.com/problems/design-circular-queue/"
					target="_blank"
					class="text-blue-500 hover:text-blue-400">Design Circular Queue</a
				> problem.
			</p>
		</div>
	</div>
</section>

<!-- Section 3: Implementation / Code Snippets -->
<section class="bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Code Implementation</h2>
			<p class="mb-4 font-medium">
				A Queue can be implemented in various programming languages. Below are examples of Queue
				implementations in Python, C++, Java, and Go:
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
					Go
				</button>
			</div>

			<div class="shadow-2xl mb-10">
				{#key codeLang}
					<CodeBlock language={codeLang} {code} />
				{/key}
			</div>

			<p class="text-xs text-gray-200 mt-2 text-center">
				Note: The implementation is for educational purposes. For production use, consider using
				built-in data structures provided by your programming language.
			</p>
		</div>
	</div>
</section>

<!-- Section 4: When to Use and When Not to Use -->
<section class="bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">
				When should a Queue be used?
			</h2>

			<p class="mb-10 font-medium">
				Queues are particularly useful when you need to process data in the order it was received.
				For example, a queue can be used to process requests on a web server. The first request
				received is the first to be processed.
			</p>

			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">
				When should a Queue be avoided?
			</h2>

			<p class="mb-4 font-medium">
				Queues are not suitable for applications that require random access to elements. For
				example, if you need to access the 5th element in a queue, you would have to dequeue the
				first 4 elements before you can access the 5th element.
			</p>
		</div>
	</div>
</section>
