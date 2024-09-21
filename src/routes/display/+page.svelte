<script lang="ts">
  import { persisted } from "svelte-persisted-store";
  import { derived } from "svelte/store";

  let max = persisted("max", 38_500);
  let value = persisted("value", 0);

  const formatter = new Intl.NumberFormat("en-US", {
    style: "currency",
    currency: "USD",
    maximumSignificantDigits: 3,
  });

  const percentage = derived([max, value], ([m, v]) => (1 - v / m) * 100);
</script>

<img class="absolute" src="./background.png" alt="Background" />
<img
  class="absolute transition-[clip-path] ease-in-out duration-1000"
  style="clip-path: inset({$percentage}% 0 0 0); left: 12vw; top: 17.45vw; width: 34.25vw;"
  src="./heart.svg"
/>
<img class="absolute" src="./overlay.png" />

<div class="absolute left-[12vw] top-[47.6vw] w-[34.25vw]">
  <div class="flex justify-center">
    <h2
      class="p-1 text-4xl font-bold tracking-tight text-center bg-white border-2 border-black rounded-lg w-80 scroll-m-20 lg:text-5xl font-['Roboto_Condensed']"
    >
      {formatter.format($value)}
    </h2>
  </div>
</div>
