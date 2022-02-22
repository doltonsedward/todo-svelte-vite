<script>
    export let isChecked
</script>

<input type=checkbox checked={isChecked} on:change />

<style>
    input {
        position: relative;
        -webkit-appearance: none;
        appearance: none;
        margin: 0;
        font: inherit;
        width: 1.30em;
        height: 1.30em;
        border: 1px solid #767e7d;
        border-radius: 50%;
        transform: translateY(-0.075em);
    }

    input::before {
        position: absolute;
        top: 50%;
        left: 50%;
        content: "";
        width: 0.65em;
        height: 0.65em;
        clip-path: polygon(14% 44%, 0 65%, 50% 100%, 100% 16%, 80% 0%, 43% 62%);
        transform: scale(0) translate(-50%, -50%);
        transform-origin: bottom left;
        transition: 120ms transform ease-in-out;
        box-shadow: inset 1em 1em white;
        background-color: CanvasText;
    }

    input:checked {
        background-color: #01E1C4;
    }

    input:checked::before {
        transform: scale(1) translate(-50%, -50%);
    }

    input:focus {
        outline: max(2px, 0.15em) solid currentColor;
        outline-offset: max(2px, 0.15em);
    }

    input:disabled {
        color: #959495;
        cursor: not-allowed;
    }
</style>