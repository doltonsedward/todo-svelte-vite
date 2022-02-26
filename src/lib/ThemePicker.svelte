<script context="module">
	const currentTheme = localStorage.getItem("theme");
	if (currentTheme) 
	document.getElementsByTagName("body")[0].classList.add(currentTheme)
</script>
<script>
	import { createEventDispatcher } from "svelte";
	const dispatch = createEventDispatcher()
	
	/**
	* @param {boolean} isDark
	*/
	function setDarkTheme(isDark) {
		if (isDark) {
			localStorage.setItem("theme", "dark")
			dispatch("getTheme", { isDark: true })
			document.getElementsByTagName("body")[0].classList.add("dark")
		} else {
			localStorage.setItem("theme", "")
			dispatch("getTheme", { isDark: true })
			document.getElementsByTagName("body")[0].classList.remove("dark")
		}
	}
</script>

<div class="container">
	<input type="checkbox" />
	<button on:click={()=> setDarkTheme(false)}>Light</button>
	<button on:click={()=> setDarkTheme(true)}>Dark</button>
</div>

<style>
	
	input {
		position: relative;
		-webkit-appearance: none;
		appearance: none;
		width: 4em;
		height: 2em;
		border-radius: 24px;
		background-color: red;
	}
	
	input::before {
		content: "";
		position: absolute;
		left: 0;
		width: 20px;
		height: 20px;
		border-radius: 50%;
		background-color: blue;
	}

	.container {
		display: flex;
	}
</style>