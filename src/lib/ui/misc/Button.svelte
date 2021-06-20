<script lang="ts">
    import { createEventDispatcher } from "svelte";

    export let color: string = "green";
    export let disabled: boolean = false;
    export let fullWidth: boolean = false;

    const dispatch = createEventDispatcher();
</script>

<style lang="scss">
    .button {
        @apply px-7 py-2 rounded-lg font-bold text-lg transition duration-200 outline-none hover:shadow-lg disabled:hover:shadow-none disabled:cursor-not-allowed;
        &.green {
            @apply text-white bg-green-400 hover:bg-green-500 active:bg-green-600 disabled:bg-green-300;
        }
        &.yellow {
            @apply text-white bg-yellow-400 hover:bg-yellow-500 active:bg-yellow-600 disabled:bg-yellow-300;
        }
        &.red {
            @apply text-white bg-red-400 hover:bg-red-500 active:bg-red-600 disabled:bg-red-300;
        }
        &.blue {
            @apply text-white bg-blue-400 hover:bg-blue-500 active:bg-blue-600 disabled:bg-blue-300;
        }
        &.gray {
            @apply text-white bg-gray-400 hover:bg-gray-500 active:bg-gray-600 disabled:bg-gray-300;
        }
        &.fullWidth {
            @apply w-full;
        }

        // Hacky way around the ugly blue box on mobile browsers
        -webkit-touch-callout: none;
        -webkit-user-select: none;
        -webkit-tap-highlight-color: transparent;
        -khtml-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
    }
</style>

<button disabled={disabled} class={`button ${color} ${fullWidth ? 'fullWidth' : ''}`} on:click={() => dispatch("click")}>
    <slot></slot>
</button>
