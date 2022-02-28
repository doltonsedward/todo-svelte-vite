<script context="module">
	const currentTheme = localStorage.getItem("theme");
	if (currentTheme) 
	document.getElementsByTagName("body")[0].classList.add(currentTheme)
</script>

<script>
	import { createEventDispatcher } from "svelte";
	const dispatch = createEventDispatcher()

	function toggle(event) {
		const isChecked = event.target.checked
		if (isChecked) {
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
	<p>Light</p>
	<label class="switch">
		<input type="checkbox" on:change={toggle} />
		<span class="slider"></span>
	</label>
	<p>Dark</p>
</div>

<style>

	p {
		color: var(--white);
	}
	
	.container {
		display: flex;
		align-items: center;
		margin-top: 10px;
	}
	
	.switch {
		position: relative;
		width: 3.4em;
		height: 2em;
		border-radius: 24px;
		overflow: hidden;
		margin: 0 10px;
	}
	
	input {
		opacity: 0;
		width: 100%;
		height: 100%;
		-webkit-appearance: none;
		appearance: none;
		transition: 0.3s;
	}

	.slider {
		position: absolute;
		cursor: pointer;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		backdrop-filter: blur(16px) saturate(180%);
		-webkit-backdrop-filter: blur(16px) saturate(180%);
		background-color: var(--neumorphism-bg);
		border-radius: 12px;
		transition: 0.3s;
	}

	.slider::before {
		position: absolute;
		content: "";
		width: 25px;
		height: 25px;
		border-radius: 50%;
		top: 50%;
		transform: translate(3px, -50%);
		backdrop-filter: blur(16px) saturate(180%);
		-webkit-backdrop-filter: blur(16px) saturate(180%);
		background-color: var(--neumorphism-bg-revert);
		border-radius: 50%;
		transition: 0.3s;
	}

	input:checked + .slider::before {
		transform: translate(100%, -50%);
		transition: 0.3s;
	}
</style>