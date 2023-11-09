<script>
    import Amount from "./Amount.svelte";
    import Info from "./Info.svelte";

    export let income = "";
    export let expense = "";
    export let total = 0;
    export let list;
</script>

<h2 class="font-bold mb-5 text-xl uppercase text-center">
    Expense Tracker <Info {list} />
</h2>
<span class="flex justify-between items-center">
    <h3 class="font-medium uppercase">balance</h3>
    <h1 class="font-semibold text-2xl"><Amount {total} /></h1>
</span>

<div class="mt-1 shadow rounded p-4 flex justify-evenly items-center">
    <div>
        <span class="block font-semibold">INCOME</span>
        <span class="block font-semibold text-green-400">+{income}</span>
    </div>
    <div class="h-[40px] bg-gray-300 w-[1px]" />
    <div>
        <span class="block font-semibold">EXPENSE</span>
        <span class="block font-semibold text-red-400">{expense}</span>
    </div>
</div>
