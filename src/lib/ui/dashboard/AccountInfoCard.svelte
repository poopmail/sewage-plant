<script lang="ts">
    import { createEventDispatcher } from "svelte";

    import Button from "../misc/Button.svelte";
    import Label from "../misc/Label.svelte";

    export let username: string = "";
    export let isAdmin: boolean = false;

    let dispatch = createEventDispatcher();
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
                & div {
                    @apply mb-3 last:mb-0;
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
            <div><Button on:click={() => dispatch("changePasswordClick")} color="yellow" fullWidth>Change password</Button></div>
            <div><Button on:click={() => dispatch("deleteAccountClick")} color="red" fullWidth>Delete account</Button></div>
        </div>
    </div>
</div>
