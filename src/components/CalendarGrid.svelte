<script lang="ts">
  let year: number = $state(new Date().getFullYear());

  let monthLengths = $derived(
    Array.from({ length: 12 }, (_, m) => new Date(year, m + 1, 0).getDate()),
  );
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
            <td class="h-4 w-4 border-2 sm:h-5 sm:w-5"></td>
          {:else}
            <td></td>
          {/if}
        {/each}
      </tr>
    {/each}
  </tbody>
</table>
