<script lang="ts">
    import { createEventDispatcher } from "svelte";

    import Button from "../misc/Button.svelte";
    import TextInput from "../misc/TextInput.svelte";
    import Label from "../misc/Label.svelte";
    import Modal from "../misc/Modal.svelte";
    import SelectInput from "../misc/SelectInput.svelte";

    export let shown: boolean = false;

    // TODO: Dynamically fetch available domains (obviously, the current state is just for debugging purposes)
    let domains: string[] = ["debug1.com", "debug2.com"];

    let address: string = Math.random().toString(16).substr(2, 8);
    let domain: string = domains[0];

    let available: boolean = true;

    let dispatch = createEventDispatcher();

    // TODO: Dynamically check for address availability (obviously, the current state is just for debugging purposes)
    function checkAvailability() {
        let cur = available;
        available = null;
        setTimeout(() => (available = !cur), 500);
    }

    function submit() {
        dispatch("submit", {
            address,
            domain
        });
        address = Math.random().toString(16).substr(2, 8);
        domain = domains[0];
    }
</script>

<style lang="scss">
    .form {
        @apply mt-5;
        & .discriminator {
            @apply text-2xl font-bold text-gray-600 mx-2 inline-block;
        }
        & .domain {
            @apply inline-block;
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
        <TextInput bind:value={address} placeholder="address" />
        <div class="discriminator">
            @
        </div>
        <div class="domain">
            <SelectInput bind:value={domain}>
                {#each domains as availableDomain}
                    <option value={availableDomain}>{availableDomain}</option>
                {/each}
            </SelectInput>
        </div>
    </div>
    <div class="availability">
        <Button disabled={available === null} on:click={checkAvailability} color="blue">Check availability</Button>
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
        <Button disabled={!available} on:click={submit} fullWidth>Create mailbox</Button>
    </div>
</Modal>
