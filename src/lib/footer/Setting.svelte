<script>
    export let isSettingOpen = false
</script>

<img class:active={isSettingOpen} on:click src="icon/gear-solid.svg" alt="setting" />

<style>
    img {
        width: 2em;
    }
    
    .active {
        transform: translateY(0%) rotate(180deg);
    }

    :not(.active) {
        transform: translateY(100%);
    }
</style>