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
	<button on:click={()=> setDarkTheme(false)}>Light</button>
	<button on:click={()=> setDarkTheme(true)}>Dark</button>
</div>

<style>
	.container {
		display: flex;
	}
</style>