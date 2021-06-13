<script lang="ts">
    export let address: string = "";
    export let domain: string = "";
    export let mails: number = 0;
    export let created: Date = new Date();

    // We have to ask the browser for access to the clipboard before copying anything (not sure if this works tho as Chrome never asks me)
    async function askForClipboardPermissions() {
        try {
            const state = await navigator.permissions.query({
                name: "clipboard-write",
            });
            return state.toString() === "granted";
        } catch (error) {
            return false;
        }
    }

    // Simply copy some text to the clipboard but ask the browser for access first
    async function copy(text: string) {
        await askForClipboardPermissions();
        await navigator.clipboard.writeText(text);
    }
</script>

<style lang="scss">
    .container {
        @apply w-full flex flex-row rounded-lg transition duration-200 hover:shadow-lg ring-gray-100 ring-2;
        & .details {
            @apply mx-10 my-10 lg:my-5 flex flex-col lg:flex-row w-full;
            & > * {
                @apply mt-5 first:mt-0 lg:mt-0 lg:ml-20 lg:first:ml-0 w-1/3 first:w-2/3;
            }
            & .labelled {
                & .label {
                    @apply text-gray-400 text-sm font-semibold uppercase mb-2;
                }
                & .content {
                    @apply text-2xl font-bold text-gray-500;
                }
            }
            & .address-container {
                @apply flex flex-row items-center cursor-pointer;
                & .address,
                & .domain {
                    @apply text-lg text-gray-500 font-semibold;
                }
                & .discriminator {
                    @apply text-2xl font-bold text-gray-600 mx-2;
                }
            }
        }
    }
</style>

<div class="container">
    <div class="details">
        <div class="labelled">
            <div class="label">Address</div>
            <div on:click={() => copy(`${address}@${domain}`)} class="content address-container" title="Click to copy">
                <div class="address">{address}</div>
                <div class="discriminator">@</div>
                <div class="domain">{domain}</div>
            </div>
        </div>
        <div class="labelled">
            <div class="label">Mails</div>
            <div class="content">{mails}</div>
        </div>
        <div class="labelled unimportant">
            <div class="label">Created</div>
            <div title={created.toString()} class="content">{`${created.getMonth()}/${created.getDay()}/${created.getFullYear()}`}</div>
        </div>
    </div>
</div>
