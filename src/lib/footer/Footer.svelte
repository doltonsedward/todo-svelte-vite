<script>
    import { createEventDispatcher } from "svelte";
    import Setting from "./Setting.svelte";

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
    <Setting />
    <div class="container">
        <div class="d-flex-responsive" on:click={handleDispatch}>
            <p>Edit Text</p>
            <input class="checkbox" type=checkbox />
        </div>
    </div>
</footer>

<style>
    footer {
        width: 100%;
        position: absolute;
        bottom: 0;
        background-color: lightblue;
    }

    .container {
        padding: 0 10px 12px;
    }

    .checkbox {
        margin-left: 10px;
    }
</style>