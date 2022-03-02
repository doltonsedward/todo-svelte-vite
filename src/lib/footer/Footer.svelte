<script>
    import { createEventDispatcher } from "svelte";
    import Setting from "./Setting.svelte";

    let isSettingOpen = false

    const dispatch = createEventDispatcher();

    let editText = false

    function handleDispatch() {
        dispatch("devmode", {
            editText: !editText
        })

        editText = !editText
    }
</script>

<footer>
    <div class="inner-footer">
        <Setting {isSettingOpen} on:click={()=> isSettingOpen = !isSettingOpen} />
        <div class="container" class:active={isSettingOpen}>
            <div class="d-flex-responsive" on:click={handleDispatch}>
                <p>Edit Text</p>
                <input class="checkbox" type=checkbox />
            </div>
        </div>
    </div>
</footer>

<style>
    footer {
        color: var(--text-color);
        width: 100%;
        position: fixed;
        bottom: 0;
    }

    .inner-footer {
        padding: 0 20px;
    }
    
    .container {
        backdrop-filter: blur(16px) saturate(180%);
		-webkit-backdrop-filter: blur(16px) saturate(180%);
		background-color: var(--neumorphism-bg);
		border-radius: 12px;
		border: 1px solid var(--neumorphism-border-color);
        transform: translateY(100%);
        padding: 12px 10px 12px;
        margin-bottom: 0;
    }

    .container.active {
        transform: translateY(0%);
        margin-bottom: 10px;
    }

    .checkbox {
        margin-left: 10px;
    }
</style>