<script>
	import { websiteName } from '$lib/stores';
	import { CodeBlock } from 'svhighlight';

	let codeLang = 'Python';

	$: code = `
		${
			codeLang === 'Python'
				? `
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop()

    def peek(self):
        return self.items[-1]

    def is_empty(self):
        return self.items == []

    def size(self):
        return len(self.items)
        `
				: ''
		}

        ${
					codeLang === 'C++'
						? `
class Stack {
    private:
        vector<int> items;

    public:
        void push(int item) {
            items.push_back(item);
        }

        int pop() {
            int item = items.back();
            items.pop_back();
            return item;
        }

        int peek() {
            return items.back();
        }

        bool is_empty() {
            return items.empty();
        }

        int size() {
            return items.size();
        }
};
        `
						: ''
				}

        ${
					codeLang === 'Java'
						? `
class Stack {
    private List<Integer> items;

    public Stack() {
        items = new ArrayList<>();
    }

    public void push(int item) {
        items.add(item);
    }

    public int pop() {
        int item = items.get(items.size() - 1);
        items.remove(items.size() - 1);
        return item;
    }

    public int peek() {
        return items.get(items.size() - 1);
    }

    public boolean is_empty() {
        return items.isEmpty();
    }

    public int size() {
        return items.size();
    }
}
        `
						: ''
				}

        ${
					codeLang === 'Go'
						? `
type Stack struct {
    items []int
}

func (s *Stack) push(item int) {
    s.items = append(s.items, item)
}

func (s *Stack) pop() int {
    item := s.items[len(s.items) - 1]
    s.items = s.items[:len(s.items) - 1]
    return item
}

func (s *Stack) peek() int {
    return s.items[len(s.items) - 1]
}

func (s *Stack) is_empty() bool {
    return len(s.items) == 0
}

func (s *Stack) size() int {
    return len(s.items)
}
        `
						: ''
				}
    `;
</script>

<svelte:head>
	<title>Stacks - {websiteName}</title>
</svelte:head>

<div class="container mx-auto mb-20">
	<!-- Title -->
	<div class="flex justify-center items-center px-20 py-20">
		<h1 class="text-6xl font-bold white">Stack Data Structure</h1>
	</div>
</div>

<!-- Section 1: Explanation of the Data Structure -->
<section class="bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">
				Understanding the Stack Data Structure
			</h2>
			<p class="mb-4 font-light">
				A Stack is a linear data structure that follows the Last In First Out (LIFO) principle. The
				LIFO principle means that the last element added to the stack will be the first element
				removed from the stack. The last element added to the stack is called the top element.
			</p>
			<p class="mb-10 font-light">
				The basic operations on a Stack are push, pop, peek, is_empty, and size. The push operation
				adds an element to the top of the stack. The pop operation removes the top element from the
				stack. The peek operation returns the top element of the stack without removing it. The
				is_empty operation returns true if the stack is empty and false otherwise. The size
				operation returns the number of elements in the stack.
			</p>
		</div>
	</div>
</section>

<!-- Section 2: Complexity Analysis for Stack -->
<section class="bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Complexity Analysis</h2>
			<p class="mb-4 font-medium">
				A stack can have the following complexities, however its performance is dependent on the
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
							<td class="px-6 py-4 text-gray-200">Θ(1)</td>
							<td class="px-6 py-4 text-gray-200">Θ(n)</td>
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
				Stacks are often used in conjunction with other data structures. For example, a stack can be
				used to reverse a string. If you'd like to write a program that simulates when to use a
				stack, see LeetCode problem 20:
				<a
					href="https://leetcode.com/problems/valid-parentheses/"
					target="_blank"
					class="underline text-blue-400">Valid Parenthesis</a
				>.
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
				A Stack can be implemented in various programming languages. Below are examples of Stack
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
				When should a Stack be used?
			</h2>

			<p class="mb-10 font-medium">
				A Stack can be implemented when you need to keep track of the order of elements. For
				example, a stack can be used to keep track of the order of web pages visited in a browser. A
				stack can also be used to keep track of the order of function calls in a program.
			</p>

			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">
				When should a Stack be avoided?
			</h2>

			<p class="mb-4 font-medium">
				A Stack should be avoided when you need to access elements in a non-sequential manner. For
				example, if you need to access the middle element of a stack, you would need to pop all the
				elements above it. This would be inefficient. In this case, a linked list would be a better
				choice.
			</p>
		</div>
	</div>
</section>
