<script lang="ts">
  import { base } from "$app/paths";

  import { Label } from "$lib/components/ui/label";
  import { Input } from "$lib/components/ui/input";
  import { persisted } from "svelte-persisted-store";

  import Button from "$lib/components/ui/button/button.svelte";

  const max = persisted("max", 38_500);
  const value = persisted("value", 0);
  let adjustment = 100;

  function add() {
    const amount = Math.max(adjustment || 0, 0);
    $value = $value + amount;
  }

  function subtract() {
    const amount = Math.max(adjustment || 0, 0);
    $value = Math.max($value - amount, 0);
  }

  const formatter = new Intl.NumberFormat("en-US", {
    style: "currency",
    currency: "USD",
    maximumSignificantDigits: 3,
  });

</script>

<div
  class="flex flex-col items-center justify-center w-full h-screen p-4 space-y-8"
>
  <div class="flex w-full max-w-sm flex-col gap-1.5">
    <Label for="max">$ Goal</Label>
    <Input id="max" type="number" bind:value={$max} />
  </div>
  <h1 class="text-4xl font-extrabold tracking-tight scroll-m-20 lg:text-5xl">
    {formatter.format($value)}
  </h1>
  <div class="flex w-full max-w-sm flex-col gap-1.5">
    <Label for="adjustment">Amount</Label>
    <Input id="adjustment" type="number" min="0" bind:value={adjustment} />
  </div>
  <div class="flex space-x-2">
    <Button size="lg" variant="default" on:click={add}>Add</Button>
    <Button size="lg" variant="destructive" on:click={subtract}>Subtract</Button>
  </div>
</div>

<Button class="absolute bottom-2 left-2" href="{base}/display" target="_blank">
  Open Display
</Button>
