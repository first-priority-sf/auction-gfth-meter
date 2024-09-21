<script lang="ts">
  import { Label } from "$lib/components/ui/label";
  import { Input } from "$lib/components/ui/input";
  import { persisted } from "svelte-persisted-store";
  import Button from "$lib/components/ui/button/button.svelte";

  const max = persisted("max", 38_500);
  const value = persisted("value", 0);

  function add(amount: number) {
    return () => {
      $value = Math.min($value + amount, $max);
    };
  }

  function subtract(amount: number) {
    return () => {
      $value = Math.max($value - amount, 0);
    };
  }

  const formatter = new Intl.NumberFormat("en-US", {
    style: "currency",
    currency: "USD",
  });
</script>

<div
  class="flex flex-col p-4 space-y-8 w-full h-screen justify-center items-center"
>
  <div class="flex w-full max-w-sm flex-col gap-1.5">
    <Label for="max">$ Goal</Label>
    <Input id="max" type="number" bind:value={$max} />
  </div>
  <h1 class="scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl">
    {formatter.format($value)}
  </h1>
  <div class="flex space-x-2">
    <Button size="lg" variant="default" on:click={add(100)}>+ $100</Button>
    <Button size="lg" variant="default" on:click={add(250)}>+ $250</Button>
    <Button size="lg" variant="default" on:click={add(500)}>+ $500</Button>
    <Button size="lg" variant="default" on:click={add(1000)}>+ $1,000</Button>
    <Button size="lg" variant="default" on:click={add(2000)}>+ $2,000</Button>
    <Button size="lg" variant="default" on:click={add(5000)}>+ $5,000</Button>
    <Button size="lg" variant="default" on:click={add(10000)}>+ $10,000</Button>
  </div>
  <div class="flex space-x-2">
    <Button size="lg" variant="destructive" on:click={subtract(100)}
      >- $100</Button
    >
    <Button size="lg" variant="destructive" on:click={subtract(250)}
      >- $250</Button
    >
    <Button size="lg" variant="destructive" on:click={subtract(500)}
      >- $500</Button
    >
    <Button size="lg" variant="destructive" on:click={subtract(1000)}
      >- $1,000</Button
    >
    <Button size="lg" variant="destructive" on:click={subtract(2000)}
      >- $2,000</Button
    >
    <Button size="lg" variant="destructive" on:click={subtract(5000)}
      >- $5,000</Button
    >
    <Button size="lg" variant="destructive" on:click={subtract(10000)}
      >- $10,000</Button
    >
  </div>
</div>

<Button
  class="absolute bottom-2 left-2"
  href="/display"
  target="_blank"
  on:click={subtract(10000)}>Open Display</Button
>
