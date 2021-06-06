<script lang="ts">
    import { createEventDispatcher } from "svelte";

    export let color: string = "green";

    const dispatch = createEventDispatcher();
</script>

<button class={`button ${color}`} on:click={() => dispatch("click")}
    ><slot /></button
>

<style lang="scss">
    .button {
        @apply px-7 py-2 rounded-2xl font-bold text-lg transition duration-200 outline-none hover:shadow-lg;
        &.green {
            @apply text-white bg-green-400 hover:bg-green-500 active:bg-green-600;
        }
        &.yellow {
            @apply text-white bg-yellow-400 hover:bg-yellow-500 active:bg-yellow-600;
        }
        &.red {
            @apply text-white bg-red-400 hover:bg-red-500 active:bg-red-600;
        }
        &.blue {
            @apply text-white bg-blue-400 hover:bg-blue-500 active:bg-blue-600;
        }
        &.gray {
            @apply text-white bg-gray-400 hover:bg-gray-500 active:bg-gray-600;
        }
    }
</style>
