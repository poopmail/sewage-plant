<script lang="ts">
    import AccountInfoCard from "$lib/ui/dashboard/AccountInfoCard.svelte";
    import MailboxCreationModal from "$lib/ui/dashboard/MailboxCreationModal.svelte";
    import MailboxLink from "$lib/ui/dashboard/MailboxLink.svelte";
    import Button from "$lib/ui/misc/Button.svelte";
    import Modal from "$lib/ui/misc/Modal.svelte";

    /**
     * ##############################
     * ##### MAILBOX LOADING ########
     * ##############################
     */
    // TODO: Dynamically fetch mailboxes (obviously, the current state is just for debugging purposes)
    let fullMailboxes: any[] = [
        {
            address: "affe",
            domain: "poopmail.pm",
            mails: 20,
            created: new Date(),
        },
        {
            address: "zerrrro",
            domain: "poopmail.pm",
            mails: 96420,
            created: new Date(),
        },
        {
            address: "i-love",
            domain: "poopmail.pm",
            mails: 42069,
            created: new Date(),
        },
        {
            address: "krokas",
            domain: "poopmail.pm",
            mails: 420,
            created: new Date(),
        },
        {
            address: "please-join",
            domain: "poopmail.pm",
            mails: 69,
            created: new Date(),
        },
    ];
    let mailboxes = fullMailboxes;
    function refreshMailboxes() {
        let newMailboxes = !mailboxes || mailboxes.length === 0 ? fullMailboxes : [];
        mailboxes = null;
        setTimeout(() => mailboxes = newMailboxes, 500);
    }

    /**
     * ##############################
     * ##### MAILBOX CREATION #######
     * ##############################
     */
    let openedCreationModal: boolean = false;
    function openCreationModal() {
        openedCreationModal = true;
    }
    function closeCreationModal() {
        openedCreationModal = false;
    }

    /**
     * ##############################
     * ##### ACCOUNT LOGOUT #########
     * ##############################
     */
    function logout() {
        // TODO: Implement logout
    }

    /**
     * ##############################
     * ##### PASSWORD CHANGE ########
     * ##############################
     */
    let openedPasswordChangeModal: boolean = false;
    function openPasswordChangeModal() {
        openedPasswordChangeModal = true;
    }
    function closePasswordChangeModal() {
        openedPasswordChangeModal = false;
    }
</script>

<style lang="scss">
    .container {
        @apply flex flex-row;
        & > * {
            @apply m-10 sm:m-20;
            & .header {
                @apply flex flex-col md:flex-row justify-between mb-10;
                & h1 {
                    @apply mb-5 md:my-auto text-xl font-semibold uppercase text-gray-500;
                }
                & .buttons {
                    @apply flex md:block;
                    & * {
                        @apply w-1/2 md:w-auto inline-block mr-3.5 last:mr-0;
                    }
                }
            }
            & .spinner {
                @apply flex justify-center mt-20;
                & svg {
                    @apply animate-spin;
                }
            }
            & .empty {
                @apply font-semibold;
            }
            & .item {
                @apply mb-7 last:mb-0;
            }
        }
        & .mailboxes {
            @apply w-full xl:w-3/4;
        }
        & .account {
            @apply w-1/4 ml-0 hidden xl:block;
        }
    }
</style>

<svelte:head>
    <title>Dashboard - PoopMail</title>
</svelte:head>

<div class="container">
    <div class="mailboxes">
        <div class="header">
            <h1>Mailboxes</h1>
            <div class="buttons">
                <div><Button disabled={mailboxes === null} on:click={refreshMailboxes} fullWidth>Refresh</Button></div>
                <div>
                    <Button on:click={openCreationModal} color="blue" fullWidth>Create new</Button>
                    <MailboxCreationModal shown={openedCreationModal} on:close={closeCreationModal}></MailboxCreationModal>
                </div>
            </div>
        </div>
        {#if mailboxes === null}
            <div class="spinner">
                <svg xmlns="http://www.w3.org/2000/svg" width="44" height="44" viewBox="0 0 24 24" stroke-width="1.5" stroke="#2c3e50" fill="none" stroke-linecap="round" stroke-linejoin="round">
                    <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
                    <path d="M4.05 11a8 8 0 1 1 .5 4m-.5 5v-5h5" />
                </svg>
            </div>
        {:else if mailboxes.length === 0}
            <span class="empty">No mailboxes found.</span>
        {:else}
            {#each mailboxes as mailbox}
                <div class="item">
                    <a href={`/mailbox/${mailbox.address}@${mailbox.domain}`}><MailboxLink
                        address={mailbox.address}
                        domain={mailbox.domain}
                        mails={mailbox.mails}
                        created={mailbox.created}
                    /></a>
                </div>
            {/each}
            <div class="item">
                <Button fullWidth disabled>Load more</Button>
            </div>
        {/if}
    </div>
    <div class="account">
        <div class="header">
            <h1>Account</h1>
            <div class="buttons">
                <div><Button on:click={logout} color="red">Log out</Button></div>
            </div>
        </div>
        <div class="item">
            <AccountInfoCard on:changePasswordClick={openPasswordChangeModal} username="Krokas der Allmächtige"></AccountInfoCard>
            <Modal shown={openedPasswordChangeModal} on:close={closePasswordChangeModal} title="TODO">TODO</Modal>
        </div>
    </div>
</div>
