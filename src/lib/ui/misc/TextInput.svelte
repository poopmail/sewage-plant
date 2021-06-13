<script lang="ts">
    export let placeholder: string = "";

    export let value: string = "";
</script>

<style lang="scss">
    input {
        @apply outline-none px-5 py-3 bg-gray-200 rounded-xl transition duration-200;
        &:focus {
            @apply shadow-md;
        }
    }
</style>

<input bind:value={value} placeholder={placeholder} type="text" />
