<script>
  import { onMount } from "svelte";

  let products = [];
  let name = "";
  let stock = 0;

  const API = "https://REPLIT_URL_HERE/products";

  async function fetchProducts() {
    const res = await fetch(API);
    products = await res.json();
  }

  async function addProduct() {
    await fetch(API, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ id: Date.now().toString(), name, stock: +stock }),
    });

    name = "";
    stock = 0;
    await fetchProducts();
  }

  onMount(fetchProducts);
</script>

<h1>Products</h1>

<input bind:value={name} placeholder="Product name" />
<input type="number" bind:value={stock} placeholder="Stock" />
<button on:click={addProduct}>Add Product</button>

<ul>
  {#each products as p}
    <li>{p.name} — {p.stock}</li>
  {/each}
</ul>
