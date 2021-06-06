<script lang="ts">
    import Button from "../misc/Button.svelte";
    import Label from "../misc/Label.svelte";

    export let domains: string[] = ["debug1.com", "debug2.com"];

    let address: string = Math.random().toString(16).substr(2, 8);
    let domain: string = "";

    let available: boolean = true;

    function checkAvailability() {
        let cur = available;
        available = null;
        setTimeout(() => (available = !cur), 500);
    }
</script>

<div class="container">
    <h1>Create mailbox</h1>
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
</div>

<style lang="scss">
    .container {
        @apply w-full p-10 rounded-lg ring-gray-100 ring-2;
        & h1 {
            @apply text-xl font-bold text-gray-600;
        }
        & .form {
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
        & .availability {
            @apply mt-5;
            & .label {
                @apply inline-block ml-5;
            }
        }
        & .creation {
            @apply mt-10;
        }
    }
</style>
