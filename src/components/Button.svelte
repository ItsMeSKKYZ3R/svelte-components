<script lang="ts">
    export let text: string | number | boolean;
    export let type: "button" | "submit" | "reset" | null | undefined = undefined;
    // export let onclick: any = undefined;
    export let style: "modern" | "round";
</script>

<button {type} class={style} on:click on:dblclick>{text}</button>

<style>
    button {
        border: none;
    }
    .modern {
        color: red;
    }
</style>