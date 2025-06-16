<script>
  import { onMount } from "svelte";

  let products = [];
  let name = "";
  let stock = 0;

  onMount(async () => {
    const res = await fetch(
      "https://9aa78eb4-d2e3-415a-ae97-074fc8ff817b-00-2eiufupxwq1ht.picard.replit.dev/products",
    );
    products = await res.json();
  });

  async function addProduct() {
    await fetch(
      "https://9aa78eb4-d2e3-415a-ae97-074fc8ff817b-00-2eiufupxwq1ht.picard.replit.dev/products",
      {
        method: "POST",
        body: JSON.stringify({
          id: Date.now().toString(),
          name,
          stock: parseInt(stock),
        }),
        headers: { "Content-Type": "application/json" },
      },
    );

    name = "";
    stock = 0;
    // Refresh
    const res = await fetch(
      "https://9aa78eb4-d2e3-415a-ae97-074fc8ff817b-00-2eiufupxwq1ht.picard.replit.dev/products",
    );
    products = await res.json();
  }
</script>

<h1>Products</h1>
<input bind:value={name} placeholder="Name" />
<input type="number" bind:value={stock} placeholder="Stock" />
<button on:click={addProduct}>Add</button>

<ul>
  {#each products as p}
    <li>{p.name} - {p.stock}</li>
  {/each}
</ul>
