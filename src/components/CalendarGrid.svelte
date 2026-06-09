<script lang="ts">
  import { entries, palette, year } from "../lib/state.svelte";

  import CellValueDialog from "./CellValueDialog.svelte";

  const months = Array.from({ length: 12 }, (_, i) => i);
  const days = Array.from({ length: 31 }, (_, i) => i);

  let monthLengths = $derived(
    Array.from({ length: 12 }, (_, month) =>
      new Date(year.value, month + 1, 0).getDate(),
    ),
  );

  function getDateKey(
    year: number,
    monthIndex: number,
    dayIndex: number,
  ): string {
    return `${year}-${String(monthIndex + 1).padStart(2, "0")}-${String(dayIndex + 1).padStart(2, "0")}`;
  }

  function closeDialog() {
    selectedCell = null;
  }

  let selectedCell = $state<string | null>(null);
</script>

<table class="border-collapse">
  <thead>
    <tr>
      <th></th>
      {#each months as month}
        <th class="text-xs">{month + 1}</th>
      {/each}
    </tr>
  </thead>

  <tbody>
    {#each days as day}
      <tr>
        <th class="pr-1.5 text-xs">{day + 1}</th>
        {#each months as month}
          {#if day < monthLengths[month]}
            <td
              class="h-4 w-4 border-2 sm:h-5 sm:w-5"
              style:background={palette[
                entries[getDateKey(year.value, month, day)]
              ]?.color}
              style:anchor-name={getDateKey(year.value, month, day) ===
              selectedCell
                ? "--selected-cell"
                : null}
              title={palette[entries[getDateKey(year.value, month, day)]]
                ?.label}
              onclick={() => {
                selectedCell = getDateKey(year.value, month, day);
              }}
            ></td>
          {:else}
            <td></td> <!-- Necessary for table alignment-->
          {/if}
        {/each}
      </tr>
    {/each}
  </tbody>
</table>

<CellValueDialog {selectedCell} {closeDialog} />
