<script lang="ts">
    import MailboxCreationModal from "$lib/ui/dashboard/MailboxCreationModal.svelte";
    import MailboxLink from "$lib/ui/dashboard/MailboxLink.svelte";
    import Button from "$lib/ui/misc/Button.svelte";
    import Label from "$lib/ui/misc/Label.svelte";
</script>

<div class="card">
    <h1>Buttons</h1>
    <div class="content">
        <div><Button>Default</Button></div>
        <div><Button color="green">Green</Button></div>
        <div><Button color="yellow">Yellow</Button></div>
        <div><Button color="red">Red</Button></div>
        <div><Button color="blue">Blue</Button></div>
        <div><Button color="gray">Gray</Button></div>
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
        <div>
            <MailboxLink
                address="some-address"
                domain="some-domain.com"
                mails={100}
            />
        </div>
        <div>
            <MailboxLink
                address="some-other-address"
                domain="some-other-domain.com"
                mails={200}
            />
        </div>
    </div>
</div>

<div class="card">
    <h1>Mailbox Creation Modal</h1>
    <div class="content">
        <div><MailboxCreationModal /></div>
    </div>
</div>

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
