<script lang="ts">
  import { palette } from "../lib/state.svelte";
</script>

<div
  class="flex flex-wrap justify-center gap-x-4 gap-y-1.5 sm:flex-col sm:items-start sm:justify-start"
>
  {#each palette as paletteValue}
    <div class="flex items-center gap-2">
      <label
        class="border-text size-6 cursor-pointer border-2"
        style:background={paletteValue.color}
      >
        <input
          type="color"
          class="absolute inset-0 cursor-pointer opacity-0"
          bind:value={paletteValue.color}
        />
      </label>

      <span
        role="textbox"
        contenteditable
        bind:innerText={paletteValue.label}
        class="py-1.5 text-sm underline underline-offset-[3px] sm:text-base"
      ></span>
    </div>
  {/each}
</div>
