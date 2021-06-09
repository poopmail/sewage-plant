<script lang="ts">
    import Button from "../misc/Button.svelte";
    import Label from "../misc/Label.svelte";

    export let username: string = "";
    export let isAdmin: boolean = false;
</script>

<style lang="scss">
    .container {
        @apply p-10 rounded-lg transition duration-200 hover:shadow-lg ring-gray-100 ring-2;
        & .labelled {
            @apply mb-10 last:mb-0;
            & .label {
                @apply text-gray-400 text-sm font-semibold uppercase mb-2;
            }
            & .content {
                @apply text-2xl font-bold text-gray-500;
                &.hasLabel {
                    @apply text-base pt-2;
                }
            }
        }
    }
</style>

<div class="container">
    <div class="labelled">
        <div class="label">Username</div>
        <div class="content">{username}</div>
    </div>
    <div class="labelled">
        <div class="label">Role</div>
        <div class="content hasLabel">
            {#if isAdmin}
                <Label color="red">Admin</Label>    
            {:else}
                <Label>User</Label>
            {/if}
        </div>
    </div>
    <div class="labelled">
        <div class="label">Actions</div>
        <div class="content">
            <div><Button color="yellow" fullWidth>Change password</Button></div>
        </div>
    </div>
</div>
