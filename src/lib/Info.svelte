<script>
    import { toast } from "svelte-sonner";

    export let list;

    let info = true;
    let imp = false;
    let exp = false;
    let value = "";

    function toggle(n) {
        switch (n) {
            case 1:
                info = true;
                imp = false;
                exp = false;
                break;

            case 2:
                info = false;
                exp = true;
                imp = false;
                break;

            case 3:
                info = false;
                exp = false;
                imp = true;
                break;
        }
    }

    function exportText() {
        const rec = localStorage.getItem("expense-tracker-record");
        if (rec) {
            navigator.clipboard.writeText(rec);
            toast.success("copied to clipboard 📋");
        } else {
            toast.warning("No record to export!");
        }
    }

    function importData() {
        if (value == "") {
            return;
        }

        try {
            let arr = JSON.parse(value);
            let data = [...arr, ...list];
            localStorage.setItem(
                "expense-tracker-record",
                JSON.stringify(data),
            );
            toast.success("successfully imported record");
            value = "";
        } catch (error) {
            toast.error("format not correct");
        }
    }
</script>

<!-- The button to open modal -->
<label for="info" class="cursor-pointer ml-1">
    <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        class="w-4 h-4 stroke-current"
        ><path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
        /></svg
    >
</label>

<!-- Put this part before </body> tag -->
<input type="checkbox" id="info" class="modal-toggle" />
<div class="modal">
    <div class="modal-box">
        {#if info}
            <div class="text-sm font-normal text-center">
                <span class="block">
                    Save data in your mobile browser not in cloud database.
                </span>
                <span
                    class="mt-2 mb-8 block px-1 bg-gray-300 w-fit mx-auto rounded"
                >
                    your data. your browser. your responsibility
                </span>
                <div class="flex items-center justify-evenly">
                    <a
                        href="https://www.linkedin.com/in/muhammad-zeeshan-801448144"
                        target="_blank"
                    >
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            viewBox="0 0 24 24"
                            fill="currentColor"
                            class="h-6 w-6"
                            aria-hidden="true"
                            ><path
                                d="M20.5 2h-17A1.5 1.5 0 002 3.5v17A1.5 1.5 0 003.5 22h17a1.5 1.5 0 001.5-1.5v-17A1.5 1.5 0 0020.5 2zM8 19H5v-9h3zM6.5 8.25A1.75 1.75 0 118.3 6.5a1.78 1.78 0 01-1.8 1.75zM19 19h-3v-4.74c0-1.42-.6-1.93-1.38-1.93A1.74 1.74 0 0013 14.19a.66.66 0 000 .14V19h-3v-9h2.9v1.3a3.11 3.11 0 012.7-1.4c1.55 0 3.36.86 3.36 3.66z"
                            /></svg
                        >
                    </a>
                    <a href="https://github.com/zexhan17" target="_blank">
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            viewBox="0 0 16 16"
                            fill="currentColor"
                            class="h-6 w-6"
                            aria-hidden="true"
                            ><path
                                d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"
                            /></svg
                        >
                    </a>
                    <a href="https://zexhan.hashnode.dev" target="_blank">
                        <svg
                            class="h-6 w-6 fill-current"
                            viewBox="0 0 200 200"
                            fill="none"
                            ><path
                                fill-rule="evenodd"
                                clip-rule="evenodd"
                                d="M13.742 66.824c-18.323 18.323-18.323 48.029 0 66.352l53.082 53.082c18.323 18.323 48.029 18.323 66.352 0l53.082-53.082c18.323-18.323 18.323-48.03 0-66.352l-53.082-53.082c-18.323-18.323-48.03-18.323-66.352 0L13.742 66.824zm109.481 56.399c12.826-12.826 12.826-33.62 0-46.446s-33.62-12.826-46.446 0-12.826 33.62 0 46.446 33.62 12.826 46.446 0z"
                            /></svg
                        >
                    </a>
                    <a
                        target="_blank"
                        href="https://portfolio-zexhan17s-projects.vercel.app"
                        download>Portfolio</a
                    >
                </div>
            </div>
        {/if}

        {#if exp}
            <div class="text-sm font-normal">
                <span class="block">
                    In case you want to reset your browser or want to transfer
                    your record to other browser you just have to export it from
                    here and import there. Export button copy all record into
                    your clipboard you can save it anywhere.
                </span>

                <button
                    class="btn btn-primary btn-sm mt-3"
                    on:click={exportText}>export</button
                >
            </div>
        {/if}

        {#if imp}
            <div class="text-sm font-normal">
                <div class="form-control">
                    <label class="label">
                        <span class="label-text">Paste Here</span>
                    </label>
                    <textarea
                        class="textarea textarea-bordered h-24"
                        bind:value
                    />
                </div>
                <button
                    class="btn btn-primary btn-sm mt-3"
                    on:click={importData}>import</button
                >
            </div>
        {/if}

        <div class="flex justify-evenly items-baseline mt-8 pt-5 border-t">
            <span
                on:click={() => toggle(1)}
                class="{info
                    ? 'underline'
                    : ''} font-normal text-sm cursor-pointer"
            >
                INFO
            </span>
            <span
                class="{exp
                    ? 'underline'
                    : ''} font-normal text-sm cursor-pointer ml-3"
                on:click={() => toggle(2)}
            >
                EXPORT
            </span>
            <span
                class="{imp
                    ? 'underline'
                    : ''} font-normal text-sm cursor-pointer ml-3"
                on:click={() => toggle(3)}
            >
                IMPORT
            </span>
        </div>
    </div>
    <label class="modal-backdrop" for="info">Close</label>
</div>
