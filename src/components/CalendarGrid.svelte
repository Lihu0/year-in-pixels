<script lang="ts">
  import { entries, palette, year } from "../lib/state.svelte";

  import CellValueDialog from "./CellValueDialog.svelte";

  const months = Array.from({ length: 12 }, (_, i) => i);
  const days = Array.from({ length: 31 }, (_, i) => i);

  let monthLengths = $derived(
    Array.from({ length: 12 }, (_, month) =>
      new Date(year.value, month + 1, 0).getDate(),
    ), // Day 0 of next month = last day of current month
  );

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
            {const key = $derived(
              `${year.value}-${String(month + 1).padStart(2, "0")}-${String(day + 1).padStart(2, "0")}`,
            )}

            <td
              class="size-4 border-2 sm:size-5"
              style:background={palette[entries[key]]?.color}
              style:anchor-name={key === selectedCell
                ? "--selected-cell"
                : null}
              title={palette[entries[key]]?.label}
              onclick={() => {
                selectedCell = key;
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
