<script>
    import { onMount } from "svelte";

    let value;

    onMount(() => {
        value = localStorage.getItem("wallet");
    });

    function handleChange(e) {
        localStorage.setItem("wallet", String(e.target.value));
    }
    $: hide = true;
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
        <h3 class="font-bold text-lg">Hidden Wallet Record!</h3>
        <p class="py-4">This record is not being used in any calculation.</p>

        <div class="form-control w-full relative">
            <label class="label">
                <span class="label-text">Amount</span>
            </label>
            <input
                type={hide ? "password" : "number"}
                {value}
                placeholder="Enter text"
                class="input input-bordered w-full"
                on:input={(e) => handleChange(e)}
            />
            <div
                class="absolute right-2 bottom-3 hover:cursor-pointer"
                on:click={() => (hide = !hide)}
            >
                {#if hide}
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke-width="1.5"
                        stroke="currentColor"
                        class="w-6 h-6"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M2.036 12.322a1.012 1.012 0 0 1 0-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178Z"
                        />
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"
                        />
                    </svg>
                {:else}
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke-width="1.5"
                        stroke="currentColor"
                        class="w-6 h-6"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            d="M3.98 8.223A10.477 10.477 0 0 0 1.934 12C3.226 16.338 7.244 19.5 12 19.5c.993 0 1.953-.138 2.863-.395M6.228 6.228A10.451 10.451 0 0 1 12 4.5c4.756 0 8.773 3.162 10.065 7.498a10.522 10.522 0 0 1-4.293 5.774M6.228 6.228 3 3m3.228 3.228 3.65 3.65m7.894 7.894L21 21m-3.228-3.228-3.65-3.65m0 0a3 3 0 1 0-4.243-4.243m4.242 4.242L9.88 9.88"
                        />
                    </svg>
                {/if}
            </div>
        </div>
    </div>
    <label class="modal-backdrop" for="wallet">Close</label>
</div>
