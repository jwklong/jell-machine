<script lang="ts">
    import { Stack } from "@utils/stack";
    import { on } from "../keys";

    export let visible: boolean;
    export let layers: Stack<string>;

    on("escape").when(() => visible).down(() => layers = layers.back());

    const actions = [
        ["Left click", "place cell"],
        ["Right click", "delete cell"],
        ["Shift+click", "edit placables"],
        ["WASD", "move camera"],
        ["Arrow keys", "move camera"],
        ["Scroll", "zoom"],
        ["Q or E", "rotate cell"],
        ["Ctrl+drag", "select area"],
        ["Cmd/Ctrl+C", "copy selected area"],
        ["Cmd/Ctrl+X", "cut selected area"],
        ["Cmd/Ctrl+V", "paste"],
        ["Alt+Arrow keys", "move selected area"],
        ["Q and E while pasting", "rotate selection"],
        ["R and F while pasting", "flip selection"],
        ["ESC", "open menu"],
        ["F1", "toggle UI around cells"],
        ["F2", "toggle grid"],
        ["F3", "toggle debug menu"],
        ["Space", "toggle simulation"],
        ["G", "Step one tick"],
        ["T", "Reset"],
    ];
</script>

<style lang="scss">
    .overlay_container {
        background-color: #363636;
        left: 0;
        position: fixed;
        top: 0;
        z-index: 102;
        width: 100%;
        height: 100%;
    }

    .overlay {
        color: #fff;
        font: 400 17px/20px "Roboto", sans-serif;
        left: 35%;
        height: auto;
        padding: 20px;
        position: fixed;
        top: 50%;
        transform: translateY(-50%);
        width: 30%;
    }

    p {
        margin: 0 0 5px 0;
    }
</style>

{#if visible}
    <div class="overlay_container">
        <div class="overlay">
            {#each actions as [trigger, what]}
                <p><b>{trigger}:</b> {what}</p>
            {/each}
            <div class="space"></div>
            <button class="center" on:click={() => layers = layers.back()}>Back</button>
        </div>
    </div>
{/if}
