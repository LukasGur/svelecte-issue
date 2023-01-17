<script lang="ts">
  import Svelecte from 'svelecte';
  let selectedValues: string[] = [];

  let products = [
    { label: 'Apple', value: 1 },
    { label: 'Banana', value: 2 },
    { label: 'Tomato', value: 3 },
    { label: 'Orange', value: 4 },
    { label: 'Juice', value: 5 },
  ];

  function handleChange(event: CustomEvent) {
    selectedValues = event.detail.map(
      (item: { label: string; value: number }) => item.value
    );
  }

  async function getNewProductValues(
    search: string
  ): Promise<{ label: string; value: number }[]> {
    console.log(search);

    // Simulate a server call
    await new Promise((resolve) => setTimeout(resolve, 300));

    return products.filter((product) => {
      return product.label.toLowerCase().includes(search.toLowerCase());
    });
  }
</script>

<div class="center">
  <Svelecte
    fetch={getNewProductValues}
    multiple
    disableSifter
    options={products}
    on:change={handleChange}
    value={selectedValues}
  />
</div>

<style>
  .center {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
</style>
