<!-- TODO: Remove this page (or at least hide it behind a simple state boolean variable) -->
<script lang="ts">
    import MailboxCreationModal from "$lib/ui/dashboard/MailboxCreationModal.svelte";
    import MailboxLink from "$lib/ui/dashboard/MailboxLink.svelte";
    import Button from "$lib/ui/misc/Button.svelte";
    import Label from "$lib/ui/misc/Label.svelte";
    import Modal from "$lib/ui/misc/Modal.svelte";

    let modalStates: boolean[] = [
        false,
        false
    ];
</script>

<style lang="scss">
    .card {
        @apply m-14 p-5 rounded-xl ring-gray-100 ring-2;
        & h1 {
            @apply mb-5 text-gray-600 text-xl font-semibold uppercase;
        }
        & .content {
            @apply flex flex-col w-max;
            & > * {
                @apply mb-5 last:mb-0;
            }
        }
    }
</style>

<div class="card">
    <h1>Buttons</h1>
    <div class="content">
        <div><Button>Default</Button><Button disabled>Default (disabled)</Button></div>
        <div><Button color="green">Green</Button><Button color="green" disabled>Green (disabled)</Button></div>
        <div><Button color="yellow">Yellow</Button><Button color="yellow" disabled>Yellow (disabled)</Button></div>
        <div><Button color="red">Red</Button><Button color="red" disabled>Red (disabled)</Button></div>
        <div><Button color="blue">Blue</Button><Button color="blue" disabled>Blue (disabled)</Button></div>
        <div><Button color="gray">Gray</Button><Button color="gray" disabled>Gray (disabled)</Button></div>
    </div>
</div>

<div class="card">
    <h1>Labels</h1>
    <div class="content">
        <div><Label>Default</Label></div>
        <div><Label color="green">Green</Label></div>
        <div><Label color="yellow">Yellow</Label></div>
        <div><Label color="red">Red</Label></div>
        <div><Label color="blue">Blue</Label></div>
        <div><Label color="gray">Gray</Label></div>
    </div>
</div>

<div class="card">
    <h1>Mailbox Links</h1>
    <div class="content">
        <div><MailboxLink address="some-address" domain="some-domain.com" mails={100}></MailboxLink></div>
        <div><MailboxLink address="some-other-address" domain="some-other-domain.com" mails={200}></MailboxLink></div>
    </div>
</div>

<div class="card">
    <h1>Modals</h1>
    <div class="content">
        <div>
            <Button on:click={() => modalStates[0] = true}>Show bare modal</Button>
            <Modal shown={modalStates[0]} on:close={() => modalStates[0] = false} title="Bare modal">Hello, world!</Modal>
        </div>
        <div>
            <Button on:click={() => modalStates[1] = true}>Show mailbox creation modal</Button>
            <MailboxCreationModal shown={modalStates[1]} on:close={() => modalStates[1] = false}></MailboxCreationModal>
        </div>
    </div>
</div>