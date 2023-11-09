<script>
    export let list;
    import { createEventDispatcher } from "svelte";
    import { toast } from "svelte-sonner";
    const dispatch = createEventDispatcher();

    let text = "";
    let amount = "";

    function save() {
        if (text == "" || amount == "") {
            toast.warning("Both fields are required");
            return;
        }
        const data = {
            id: crypto.randomUUID(),
            text,
            amount: parseFloat(amount),
            date: new Date(),
        };
        dispatch("addNewITem", data);

        text = "";
        amount = "";

        toast.success("success!");
    }

    function formatDate(inputDate) {
        const months = [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
            "Oct",
            "Nov",
            "Dec",
        ];

        const dateObj = new Date(inputDate);
        const day = String(dateObj.getDate()).padStart(2, "0");
        const month = months[dateObj.getMonth()];
        const year = dateObj.getFullYear();
        const hours = dateObj.getHours() % 12 || 12;
        const minutes = String(dateObj.getMinutes()).padStart(2, "0");
        const ampm = dateObj.getHours() >= 12 ? "PM" : "AM";

        const formattedDate = `${day}-${month}-${year}, ${hours}:${minutes} ${ampm}`;
        return formattedDate;
    }
</script>

<div class="flex justify-between items-baseline">
    {#if list.length > 0}
        <h1 class="font-semibold mt-5">History</h1>
    {/if}
    <label for="my_modal_6" class="btn btn-primary rounded btn-xs"> + </label>
</div>
{#if list.length > 0}
    <hr class="bg-gray-200 p-[.5px] mb-3 mt-1" />

    <ul class="space-y-3">
        {#each list as e}
            <li
                class="p-2 space-y-1 shadow rounded border-l-4 {e.amount > 0
                    ? 'border-green-400'
                    : 'border-red-400'}"
            >
                <div class="flex justify-between items-top">
                    <span>{e.text}</span>
                    <span
                        class={e.amount > 0 ? "text-green-400" : "text-red-400"}
                    >
                        {e.amount}
                    </span>
                </div>
                <div class="flex justify-between items-baseline">
                    <small class="text-xs text-gray-400 uppercase">
                        {formatDate(e.date)}
                    </small>
                    <button
                        on:click={() => dispatch("delete", e.id)}
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
            </li>
        {/each}
    </ul>
{/if}

<input type="checkbox" id="my_modal_6" class="modal-toggle" />
<div class="modal modal-bottom sm:modal-middle">
    <div class="modal-box">
        <h1 class="font-semibold">Add New Transaction</h1>
        <hr class="bg-black p-[.5px] mb-3" />
        <div class="space-y-3">
            <div class="form-control w-full">
                <label class="label">
                    <span class="label-text">Text</span>
                </label>
                <input
                    type="text"
                    placeholder="Enter text"
                    class="input input-bordered w-full"
                    bind:value={text}
                />
            </div>
            <div class="form-control w-full">
                <label class="label">
                    <span class="label-text">Amount</span>
                </label>
                <input
                    type="number"
                    placeholder="Enter Amount"
                    class="input input-bordered w-full"
                    bind:value={amount}
                />
                <label class="label">
                    <span class="label-text"
                        >positive - income, negative - expense</span
                    >
                </label>
            </div>
            <button class="btn btn-neutral w-full" on:click={save}>SAVE</button>
        </div>

        <div class="modal-action">
            <label for="my_modal_6" class="btn">Close!</label>
        </div>
    </div>
</div>
