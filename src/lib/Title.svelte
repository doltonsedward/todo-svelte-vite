<script>
    export let name = "";
    export let editable = false;

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
        <input class="input__data" bind:value={name} on:keypress={handleEnterInput} />
    {:else}
        <h2>{name}</h2>
    {/if}
    <div class="icon__edit" on:click={()=> isInputActive = !isInputActive}>
        <img class:active={editable} src="icon/edit-solid.svg" alt="edit">
    </div>
</div>


<style>
    .container {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 0 0 0.5em 0;
    }
    
    h2 {
        width: 5em;
        display: inline;
		color: whitesmoke;
		font-size: 2em;
		font-weight: 200;
		user-select: none;
	}

    .input__data {
        color: var(--default-text-color);
        width: 5em;
        font-size: 2em;
        border-bottom: 1px solid var(--neumorphism-bg-revert);
    }

    .icon__edit {
        display: grid;
        place-items: center;
        position: relative;
        width: 8%;
        height: 8%;
    }
    
    img { 
        transform: scale(0.8) translateY(15px);
        opacity: 0;
        cursor: pointer;
    }
    
    .active {
        transform: scale(1) translateY(0);
        opacity: 1;
        transition: 120ms transform opacity ease-in-out;
    }
</style>