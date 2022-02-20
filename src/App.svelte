<script>
	import { quintOut } from 'svelte/easing';
	import { crossfade } from 'svelte/transition';
	import { flip } from 'svelte/animate';
	import ThemePicker from "./lib/ThemePicker.svelte";

	let uid = 1;

	let todos = JSON.parse(localStorage.getItem("todos"))
	let dataTodos = [
		{ id: uid++, done: false, description: 'eat' },
		{ id: uid++, done: true,  description: 'buy some milk' },
		{ id: uid++, done: false, description: 'mow the lawn' },
		{ id: uid++, done: false, description: 'feed the turtle' },
		];

	if (!todos) {
		localStorage.setItem("todos", JSON.stringify(dataTodos))
		location.reload()
	}

	/**
	* @param {[]} todos
	*/
  	const setTodos = (todos) => localStorage.setItem("todos", JSON.stringify(todos))

	const [send, receive] = crossfade({
		duration: d => Math.sqrt(d * 200),

		fallback(node, params) {
			const style = getComputedStyle(node);
			const transform = style.transform === 'none' ? '' : style.transform;

			return {
				duration: 600,
				easing: quintOut,
				css: t => `
					transform: ${transform} scale(${t});
					opacity: ${t}
				`
			};
		}
	});

	/**
	* @param {any} input
	*/
	function add(input) {
    if (input.value.length < 1) return;
    
		const todo = {
			id: uid++,
			done: false,
			description: input.value
		};

		todos = [todo, ...todos];
    	setTodos(todos)
		input.value = '';
	}

	function remove(todo) {
		todos = todos.filter(t => t !== todo);
    	setTodos(todos)
	}

	function mark(todo, done) {
		todo.done = done;
		remove(todo);
		todos = todos.concat(todo);
    	setTodos(todos)
	}

	let isDarkTheme = (localStorage.getItem("theme") === "dark")

	/**
	* @param {{ detail: { isDark: boolean; }; }} event
	*/
	function handleGetTheme(event) {
		isDarkTheme = event.detail.isDark
	}
</script>

<div class="board">
	<ThemePicker on:getTheme={handleGetTheme} />
	
	<input
		placeholder="what needs to be done?"
		on:keydown={e => e.key === 'Enter' && add(e.target)}
	>

	<div class="section-left">
		<h2>todo</h2>
		{#each todos.filter(t => !t.done) as todo (todo.id)}
			<label
				in:receive="{{key: todo.id}}"
				out:send="{{key: todo.id}}"
				animate:flip
			>
				<input type=checkbox on:change={() => mark(todo, true)} />
				{todo.description}
				<button on:click="{() => remove(todo)}">
					{#if isDarkTheme}
						<img src="images/trash-light.png" alt="delete" />
					{:else}
						<img src="images/trash.png" alt="delete" />
					{/if}
				</button>
			</label>
		{/each}
	</div>

	<div class="section-right">
		<h2>done</h2>
		{#each todos.filter(t => t.done) as todo (todo.id)}
			<label
				class="done"
				in:receive="{{key: todo.id}}"
				out:send="{{key: todo.id}}"
				animate:flip
			>
				<input type=checkbox checked on:change={() => mark(todo, false)}>
				{todo.description}
				<button on:click="{() => remove(todo)}">
					{#if isDarkTheme}
						<img src="images/trash-light.png" alt="delete" />
					{:else}
						<img src="images/trash.png" alt="delete" />
					{/if}
				</button>
			</label>
		{/each}
	</div>
</div>

<style>
  	:focus { outline: none }
	::placeholder {
		opacity: 0.5;
	}
	  
	::placeholder, .board > input, label {
		color: var(--text-color);
	}

	.board {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 1em;
		max-width: 36em;
		margin: 0 auto;
	}

	.board > input {
		font-family: "Poppins";
		margin-top: 12px;
		padding: 0.5em 1em;
		font-size: 1.4em;
		grid-column: 1/3;
		backdrop-filter: blur(16px) saturate(180%);
		-webkit-backdrop-filter: blur(16px) saturate(180%);
		background-color: var(--neumorphism-bg);
		border-radius: 12px;
		border: 1px solid var(--neumorphism-border-color);
	}

	h2 {
		color: whitesmoke;
		font-size: 2em;
		font-weight: 200;
		user-select: none;
		margin: 0 0 0.5em 0;
	}

	label {
    	display: block;
		position: relative;
		line-height: 1.2;
		padding: 0.5em 2.5em 0.5em 0.5em;
		margin: 0 0 0.5em 0;
		border-radius: 2px;
		user-select: none;
		backdrop-filter: blur(16px) saturate(180%);
		-webkit-backdrop-filter: blur(16px) saturate(180%);
		background-color: var(--neumorphism-bg);
		border-radius: 12px;
		border: 1px solid var(--neumorphism-border-color);
	}

	.done {
		border: 1px solid hsl(240, 8%, 90%);
		backdrop-filter: blur(16px) saturate(180%);
		-webkit-backdrop-filter: blur(16px) saturate(180%);
		background-color: var(--success-bg);
		border: 1px solid var(--neumorphism-border-color);
	}

	button {
		display: grid;
		place-items: center;
		position: absolute;
		top: 0;
		right: 0.2em;
		width: 2em;
		height: 100%;
		background-color: transparent;
		background-size: 1.4em 1.4em;
		border: none;
		opacity: 0;
		transition: opacity 0.2s;
		cursor: pointer;
	}

	button img { width: 20px }

	label:hover button { opacity: 1 }
</style>