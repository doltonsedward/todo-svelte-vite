<script>
    export let name = ""

    let isInputActive

    /**
    * @param {{ keyCode: number; }} event
    */
    function handleEnterInput(event) {
        // if user press enter, set toggle isInputActive
        if (event.keyCode === 13) {
            isInputActive = !isInputActive
        }
    }
</script>

<div class="container">
    {#if isInputActive} 
        <input bind:value={name} on:keypress={handleEnterInput} />
    {:else}
        <h2>{name}</h2>
    {/if}
    <button on:click={()=> isInputActive = !isInputActive}>
        <div></div>
    </button>
</div>


<style>
    h2 {
        display: inline;
		color: whitesmoke;
		font-size: 2em;
		font-weight: 200;
		user-select: none;
		margin: 0 0 0.5em 0;
	}

    button{
        position: relative;
        -webkit-appearance: none;
        appearance: none;
        margin: 0;
        font: inherit;
        width: 1.30em;
        height: 1.30em;
        border: 1px solid #767e7d;
        border-radius: 50%;
    }

    button div {
        position: absolute;
        content: "";
        width: 100%;
        height: 100%;
        clip-path: polygon(14% 44%, 0 65%, 50% 100%, 100% 16%, 80% 0%, 43% 62%);
        transform: scale(0) translate(-50%, -50%);
        transform-origin: bottom left;
        transition: 120ms transform ease-in-out;
        box-shadow: inset 1em 1em white;
        background-color: CanvasText;
    }
</style>