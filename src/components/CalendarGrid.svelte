<script lang="ts">
  let year: number = $state(new Date().getFullYear());

  let palette: {
    color: string;
    label: string;
  }[] = $state([
    { color: "#C89442", label: "Great" },
    { color: "#A3C867", label: "Pretty Good" },
    { color: "#75BFD1", label: "Normal" },
    { color: "#A991DD", label: "Not So Great" },
    { color: "#DD88CC", label: "Bad" },
  ]);

  let entries: Record<string, number> = $state({
    "2026-01-01": 0,
    "2026-01-02": 1,
    "2026-01-03": 2,
    "2026-01-04": 3,
    "2026-01-05": 4,
  });

  let monthLengths = $derived(
    Array.from({ length: 12 }, (_, m) => new Date(year, m + 1, 0).getDate()),
  );

  function getDateKey(
    year: number,
    monthIndex: number,
    dayIndex: number,
  ): string {
    const month = monthIndex + 1;
    const day = dayIndex + 1;

    return `${year}-${String(month).padStart(2, "0")}-${String(day).padStart(2, "0")}`;
  }
</script>

<table class="border-collapse">
  <thead>
    <tr>
      <th></th>
      {#each Array(12) as _, i}
        <th class="text-xs">{i + 1}</th>
      {/each}
    </tr>
  </thead>

  <tbody>
    {#each Array(31) as _, day}
      <tr>
        <th class="pr-1.5 text-xs">{day + 1}</th>
        {#each Array(12) as _, month}
          {#if day < monthLengths[month]}
            <td
              class="h-4 w-4 border-2 sm:h-5 sm:w-5"
              style:background={palette[entries[getDateKey(year, month, day)]]
                ?.color ?? null}
              onclick={() => {
                entries = {
                  ...entries,
                  [getDateKey(year, month, day)]: 2, // Temporary for now
                };
              }}
            ></td>
          {:else}
            <td></td>
          {/if}
        {/each}
      </tr>
    {/each}
  </tbody>
</table>
