<script lang="ts">
  import ChevronDown from "@lucide/svelte/icons/chevron-down";

  import { entries, year } from "../lib/state.svelte";

  const years = Array.from(
    new Set([
      ...Object.keys(entries).map((d) => Number(d.slice(0, 4))),
      new Date().getFullYear(),
    ]),
  ).sort((a, b) => a - b);
</script>

<div class="flex flex-col items-center gap-1">
  <label for="year-select" class="text-xl">Year:</label>

  <div class="relative inline-block border-graphite border-3">
    <select
      name="year select"
      id="year-select"
      class="pr-10.5 appearance-none pl-6 py-1.25 font-bold text-orange-700 bg-transparent outline-none"
      bind:value={year.value}
    >
      {#each years as yearOption}
        <option value={yearOption}>
          {yearOption}
        </option>
      {/each}
    </select>

    <ChevronDown
      strokeWidth={3}
      class="pointer-events-none absolute right-2 top-1/2 size-4 -translate-y-1/2 text-orange-700"
    /> <!-- Guarantees the chevron will show in html-to-image -->
  </div>
</div>
