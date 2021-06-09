<script lang="ts">
    export let color: string = "green";
</script>

<style lang="scss">
    .label {
        @apply px-5 py-2 rounded-full font-bold uppercase;
        &.green {
            @apply bg-green-200 text-green-500;
        }
        &.yellow {
            @apply bg-yellow-200 text-yellow-600;
        }
        &.red {
            @apply bg-red-200 text-red-500;
        }
        &.blue {
            @apply bg-blue-200 text-blue-500;
        }
        &.gray {
            @apply bg-gray-200 text-gray-500;
        }
    }
</style>

<span class={`label ${color}`}>
    <slot></slot>
</span>
