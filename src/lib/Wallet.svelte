<script>
    import { onMount } from "svelte";
    import { openDatabase, fetchAllRows, addRow, deleteRow } from "./db";

    let db;
    $: wallets = [];
    const storeName = "wallets";

    onMount(async () => {
        db = await openDatabase(storeName);
        wallets = await fetchAllRows(db, storeName);
    });

    async function handleSubmit(e) {
        const formData = new FormData(e.target);
        const name = formData.get("name");
        const amount = formData.get("amount");
        const data = {
            id: wallets.length + 1,
            name,
            amount,
        };

        await addRow(db, storeName, data);
        wallets = await fetchAllRows(db, storeName);
        e.target.reset();
    }

    async function deleteWallet(id) {
        await deleteRow(db, storeName, id);
        wallets = await fetchAllRows(db, storeName);
    }
</script>

<label for="wallet" class="cursor-pointer">
    <h2
        class="font-bold my-10 text-xl uppercase flex items-center place-content-center"
    >
        Expense Tracker
    </h2>
</label>

<input type="checkbox" id="wallet" class="modal-toggle" />
<div class="modal" role="dialog">
    <div class="modal-box">
        <h3 class="font-bold text-lg">Hidden Wallets!</h3>
        <p class="pb-4">These records is not being used in any calculation.</p>

        <form
            on:submit|preventDefault={handleSubmit}
            class="form-control w-full space-y-2 border border-base-300 p-5"
        >
            <label for="name">
                Wallet Name
                <input
                    class="input input-bordered w-full"
                    type="text"
                    required
                    name="name"
                />
            </label>

            <label for="value">
                Wallet Amount
                <input
                    class="input input-bordered w-full"
                    type="number"
                    required
                    name="amount"
                />
            </label>

            <button class="btn btn-primary" type="submit">
                Add new Wallet
            </button>
        </form>

        <div class="mt-5 max-h-52 overflow-y-auto">
            <h1>Wallets</h1>
            {#each wallets as wallet}
                <div
                    class="p-2 border-b border-base-300 rounded flex items-center justify-between"
                >
                    <span>{wallet.name}: {wallet.amount}</span>
                    <button
                        on:click={() => deleteWallet(wallet.id)}
                        class="text-red-500"
                        ><svg
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke-width="1.5"
                            stroke="currentColor"
                            class="w-4 h-4"
                        >
                            <path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
                            />
                        </svg>
                    </button>
                </div>
            {/each}
        </div>
    </div>
    <label class="modal-backdrop" for="wallet">Close</label>
</div>
