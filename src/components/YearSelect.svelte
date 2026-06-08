<script lang="ts">
  import { entries, year } from "../lib/state.svelte";

  const years = Array.from(
    new Set([
      ...Object.keys(entries).map((d) => Number(d.slice(0, 4))),
      new Date().getFullYear(),
    ]),
  ).sort((a, b) => a - b);
</script>

<label for="year-select" class="flex flex-col items-center gap-1">
  <span class="font-xl">Year:</span>

  <div class="border-graphite border-3 h-10 flex items-center justify-center">
    <select
      name="year select"
      id="year-select"
      class="text-center w-24 font-bold text-orange-700 bg-transparent outline-none"
      bind:value={year.value}
    >
      {#each years as yearOption}
        <option value={yearOption}>
          {yearOption}
        </option>
      {/each}
    </select>
  </div>
</label>
