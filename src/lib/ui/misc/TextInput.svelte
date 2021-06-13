<script lang="ts">
    export let placeholder: string = "";
    export let password: boolean = false;
    export let disabled: boolean = false;
    export let fullWidth: boolean = false;

    export let value: string = "";
</script>

<style lang="scss">
    input {
        @apply outline-none px-5 py-3 bg-gray-200 rounded-xl transition duration-200;
        &:focus {
            @apply shadow-md;
        }
        &.fullWidth {
            @apply w-full;
        }
    }
</style>

{#if password}
    <input bind:value={value} disabled={disabled} class={`${fullWidth ? 'fullWidth' : ''}`} placeholder={placeholder} type="password" />
{:else}
    <input bind:value={value} disabled={disabled} class={`${fullWidth ? 'fullWidth' : ''}`} placeholder={placeholder} type="text" />
{/if}
