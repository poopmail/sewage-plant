<script lang="ts">
    export let value: string = "";
</script>

<style lang="scss">
    .container {
        & select {
            @apply outline-none px-5 pr-12 py-3 bg-gray-200 rounded-xl appearance-none cursor-pointer transition duration-200;
            &:focus {
                @apply shadow-md;
            }
        }
        &::after {
            @apply -ml-7 mr-3.5 cursor-pointer inline-block pointer-events-none;
            content: "\25bc";
        }
    }
</style>

<div class="container">
    <select bind:value={value}>
        <slot></slot>
    </select>
</div>
