<script lang="ts">
  import { persisted } from "svelte-persisted-store";
  import { derived } from "svelte/store";

  let max = persisted("max", 38_500);
  let value = persisted("value", 0);

  const percentage = derived([max, value], ([m, v]) => (1 - v / m) * 100);
</script>

<img class="absolute" src="./background.png" alt="Background" />
<img
  class="absolute transition-[clip-path] ease-in-out duration-1000"
  style="clip-path: inset({$percentage}% 0 0 0); left: 12.13vw; top: 17.38vw; width: 34.25vw;"
  src="./heart.svg"
/>
<img class="absolute" src="./overlay.png" />
