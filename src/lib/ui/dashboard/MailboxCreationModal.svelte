<script lang="ts">
    import Button from "../misc/Button.svelte";
    import Label from "../misc/Label.svelte";
    import Modal from "../misc/Modal.svelte";

    export let shown: boolean = false;

    // TODO: Dynamically fetch available domains (obviously, the current state is just for debugging purposes)
    let domains: string[] = ["debug1.com", "debug2.com"];

    let address: string = Math.random().toString(16).substr(2, 8);
    let domain: string = "";

    let available: boolean = true;

    // TODO: Dynamically check for address availability (obviously, the current state is just for debugging purposes)
    function checkAvailability() {
        let cur = available;
        available = null;
        setTimeout(() => (available = !cur), 500);
    }
</script>

<style lang="scss">
    .form {
        @apply mt-5;
        & .address {
            @apply outline-none px-5 py-3 bg-gray-200 rounded-xl transition duration-200;
            &:focus {
                @apply shadow-md;
            }
        }
        & .discriminator {
            @apply text-2xl font-bold text-gray-600 mx-2 inline-block;
        }
        & .domain {
            @apply inline-block;
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
    }
    .availability {
        @apply mt-5;
        & .label {
            @apply inline-block ml-5;
        }
    }
    .creation {
        @apply mt-10;
    }
</style>

<Modal shown={shown} on:close title="Create mailbox">
    <div class="form">
        <input bind:value={address} class="address" type="text" placeholder="address" />
        <div class="discriminator">
            @
        </div>
        <div class="domain">
            <select bind:value={domain}>
                {#each domains as availableDomain}
                    <option value={availableDomain}>{availableDomain}</option>
                {/each}
            </select>
        </div>
    </div>
    <div class="availability">
        <Button color="blue" on:click={checkAvailability}>Check availability</Button>
        <div class="label">
            {#if available === null}
                <Label color="blue">Checking...</Label>
            {:else if available}
                <Label color="green">Available</Label>
            {:else}
                <Label color="red">Unavailable</Label>
            {/if}
        </div>
    </div>
    <div class="creation">
        <Button disabled={!available}>Create mailbox</Button>
    </div>
</Modal>