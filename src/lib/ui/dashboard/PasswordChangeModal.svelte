<script lang="ts">
    import { fade } from "svelte/transition";
    import { createEventDispatcher } from "svelte";

    import Button from "../misc/Button.svelte";
    import TextInput from "../misc/TextInput.svelte";
    import Modal from "../misc/Modal.svelte";

    export let shown: boolean = false;

    let oldPassword: string = "";
    let newPassword: string = "";
    let repeatNewPassword: string = "";

    $: valid = oldPassword.length > 0 && newPassword.length > 0 && newPassword === repeatNewPassword;

    let dispatch = createEventDispatcher();

    function submit() {
        dispatch("submit", newPassword);
        oldPassword = "";
        newPassword = "";
        repeatNewPassword = "";
    }
</script>

<style lang="scss">
    .form {
        @apply mt-10;
        & > * {
            @apply mb-5 last:mb-0;
        }
    }
    .messages {
        @apply mt-10 text-red-500 font-semibold;
    }
    .action {
        @apply mt-10;
    }
</style>

<Modal shown={shown} on:close title="Change acccount password">
    <div class="form">
        <div><TextInput bind:value={oldPassword} placeholder="Old password" fullWidth password></TextInput></div>
        <div><TextInput bind:value={newPassword} placeholder="New password" fullWidth password></TextInput></div>
        <div><TextInput bind:value={repeatNewPassword} placeholder="Repeat new password" fullWidth password></TextInput></div>
    </div>
    <div class="messages">
        {#if oldPassword.length === 0}
            <div transition:fade>Please enter your old password.</div>
        {/if}
        {#if newPassword.length === 0}
            <div transition:fade>Please enter your new password.</div>
        {/if}
        {#if newPassword !== repeatNewPassword}
            <div transition:fade>The new passwords do not match.</div>
        {/if}
    </div>
    <div class="action">
        <Button fullWidth disabled={!valid} on:click={submit}>Change password</Button>
    </div>
</Modal>
