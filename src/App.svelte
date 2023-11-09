<script>
  import { Toaster, toast } from "svelte-sonner";
  import Header from "./lib/Header.svelte";
  import History from "./lib/History.svelte";
  import { onMount } from "svelte";

  let list = [];

  $: expense = list
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);

  $: income = list
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);

  $: total = list.reduce((acc, transaction) => acc + transaction.amount, 0);

  onMount(() => {
    let data = JSON.parse(localStorage.getItem("expense-tracker-record"));
    if (data) {
      list = data;
    }
  });

  function add(data) {
    list = [data.detail, ...list];
    setToLocalStorage();
  }

  function setToLocalStorage() {
    localStorage.setItem("expense-tracker-record", JSON.stringify(list));
  }

  function deleteItem(data) {
    let id = data.detail;
    list = list.filter((f) => f.id != id);
    setToLocalStorage();
    toast.success("Deleted");
  }
</script>

<main class="grid place-content-center my-10">
  <div class="w-72">
    <Header {expense} {total} {income} />
    <History {list} on:addNewITem={add} on:delete={deleteItem} />
  </div>
</main>

<Toaster position="top-center" richColors />
