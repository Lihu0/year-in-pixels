<script lang="ts">
  import SquarePlus from "@lucide/svelte/icons/square-plus";
  import X from "@lucide/svelte/icons/x";

  import { entries, palette } from "../lib/state.svelte";
</script>

<div
  class="flex flex-wrap justify-center gap-x-4 gap-y-1.5 sm:flex-col sm:items-start sm:justify-start"
>
  {#each palette as paletteValue, i}
    <div class="flex items-center gap-2">
      <button
        class="opacity-40 hover:opacity-100"
        title="Delete color"
        data-no-export
        onclick={() => {
          Object.entries(entries).forEach(([key, val]) => {
            if (val === i) delete entries[key];
            else if (val > i) entries[key]--;
          });

          palette.splice(i, 1);
        }}
      >
        <X size={16} />
      </button>

      <label
        class="border-graphite size-6 cursor-pointer border-2"
        style:background={paletteValue.color}
      >
        <input
          type="color"
          class="inset-0 cursor-pointer opacity-0 size-full"
          bind:value={paletteValue.color}
          aria-label={`Color picker for ${paletteValue.label}`}
        />
      </label>

      <span
        role="textbox"
        contenteditable
        aria-label={`Color label for ${paletteValue.label}`}
        bind:innerText={paletteValue.label}
        class="py-1.5 text-sm underline underline-offset-[3px] sm:text-base"
      ></span>
    </div>
  {/each}

  <button
    class="flex cursor-pointer items-center gap-2 text-sm opacity-40 hover:opacity-100 sm:text-base"
    title="Add color"
    data-no-export
    onclick={() => {
      palette.push({ label: "New Color", color: "#000000" });
    }}
  >
    <SquarePlus size={16} />
    <span class="underline underline-offset-[3px]">Add color</span>
  </button>
</div>
