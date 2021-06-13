<!-- TODO: Fix stupid mobile scrolling bug (I hate CSS) -->
<script lang="ts">
    import { createEventDispatcher } from "svelte";

    import { fade } from "svelte/transition";

    export let title: string = "";
    export let shown: boolean = false;
    export let closeable: boolean = true;

    let dispatch = createEventDispatcher();

    function handleKeydown(event: KeyboardEvent) {
        if (shown && closeable && event.key === "Escape") {
            dispatch("close");
        }
    }
</script>

<svelte:window on:keydown={handleKeydown}></svelte:window>

<style lang="scss">
    .wrapper {
        @apply fixed top-0 left-0 w-screen h-screen flex items-center justify-center bg-black bg-opacity-80 backdrop-filter backdrop-blur-sm;
        & .container {
            @apply p-10 rounded-lg bg-white ring-gray-100 ring-2;
            height: fit-content;
            & h1 {
                @apply text-xl font-bold text-gray-600;
            }
            & .close-icon {
                @apply fixed top-10 right-10 w-14 h-14 cursor-pointer stroke-current text-white hover:text-gray-400 transition duration-200;
            }
            & .content {
                @apply mt-5;
            }
        }
    }
</style>

{#if shown} 
    <div class="wrapper" transition:fade={{duration: 150}}>
        <div class="container">
            <h1>{title}</h1>
            {#if closeable}
                <div class="close-icon" on:click={() => dispatch("close")}>
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" stroke-width="1.5" fill="none" stroke-linecap="round" stroke-linejoin="round">
                        <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                        <rect x="4" y="4" width="16" height="16" rx="2" />
                        <path d="M10 10l4 4m0 -4l-4 4" />
                    </svg>
                </div>
            {/if}
            <div class="content"><slot></slot></div>
        </div>
    </div>
{/if}