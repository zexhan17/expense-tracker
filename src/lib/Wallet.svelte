<script>
    import { onMount } from "svelte";

    let value;

    onMount(() => {
        value = localStorage.getItem("wallet");
    });

    function handleChange(value) {
        localStorage.setItem("wallet", String(value));
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
        <h3 class="font-bold text-lg">Hello To Hidden Wallet Record!</h3>
        <p class="py-4">
            This save value is not calculated by any record not will be include
            in any calculation.
        </p>

        <div class="form-control w-full">
            <label class="label">
                <span class="label-text">Amount</span>
            </label>
            <input
                type="number"
                bind:value
                placeholder="Enter text"
                class="input input-bordered w-full"
                on:input={(e) => handleChange(e.target.value)}
            />
        </div>

        <div class="modal-action">
            <label for="wallet" class="btn">Close!</label>
        </div>
    </div>
</div>
